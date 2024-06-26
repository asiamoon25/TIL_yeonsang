Local Docker 에 K8S 로 야무지게 백엔드 배포해보기

```dockerfile
# tomcat:7.0.86 베이스 이미지 사용
FROM tomcat:7.0.86

# Jenkins 빌드 과정에서 생성된 WAR 파일을 이미지에 복사
# 이 경로는 JENKINS 작업 공간에 따라 조정해야할 수 있음.
COPY /home/happytuk/target/ROOT.war /usr/local/tomcat7/webapps/ROOT.war

# tomcat 포트 노출
EXPOSE 8080
```

### deployment 파일 작성 
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
	name: your-app-deployment
spec:
	replicas: 2
	selector:
		matchLabels:
			app: your-app
	template:
		metadata:
			labels:
				app: your-app
		spec:
			containers:
			- name: your-app
			   image: your-docker-image
			   ports:
			   - containerPort: 8080
```

### service 파일 작성
```yaml
apiVersion: v1
kind: Service
metadata:
	name: your-app-service
spec:
	type: LoadBalancer
	ports:
	- port: 80
	   targetPort: 8080
	selector:
		app: your-app
```

### JENKINS 에서 Docker 이미지 빌드 및 배포 자동화

1. Jenkins 에 Docker 플러그인 설치: Jenkins 관리 페이지에서 플러그인 관리를 통해 Docker Plugin 을 설치
2. 빌드 스크립트 작성
```sh
# 이미지 빌드
docker build -t HAPPYCODE:test .

# Docker 이미지를 Docker hub 나 다른 registry 에 push -> Azure Registry
docker push HAPPYCODE:test

# 추가적인 배포 스크립트(k8s 클러스터에 배포)
kubectl set image deployment/your-app-deployment#yaml 파일
your-app-container-name:tag # 올린 이미지
```






구조 어떻게 할건지....







----
#### 1. 기본 Tomcat Dockerfile
```dockerfile
# Tomcat 공식 이미지를 베이스 이미지로 사용
FROM tomcat:9.0

# CATALINA_OPTS 환경 변수 설정
ENV CATALINA_OPTS="-Djava.awt.headless=true -Dfile.encoding=UTF-8 -server -Xms512m -Xmx1024m -XX:+UseParallelGC"

# 원하는 WAR 파일을 Tomcat의 webapps 디렉토리로 복사
COPY path/to/your-app.war $CATALINA_HOME/webapps/your-app.war

# 컨테이너에서 노출할 포트 번호
EXPOSE 8080

# Tomcat 서버 실행
CMD ["catalina.sh", "run"]
 
```



```dockerfile
FROM tomcat:7.0.86

ENV CATALINA_OPTS="-Djava.awt.headless=true -Dfile.encoding=UTF-8 -server -Xms4096m -Xmx4096m -XX:ParallelGCThreads=2 -XX:-UseConcMarkSweepGC -XX:NewSize=1024m -XX:MaxNewSize=1024m -XX:PermSize=1G -XX:MaxPermSize=2G -XX:+DisableExplicitGC -Dfile.encoding=UTF8 -Duser.timezone=GMT+8"

COPY ./target/ROOT.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080

CMD ["startup.sh","run"]
```

JENKINS PIPELINE
```groovy
pipeline {
    agent any
    stages {
        stage('Build WAR') {
            steps {
                // Maven을 사용하는 경우
                sh 'mvn clean package'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    // Docker 이미지 빌드
                    docker.build("your-app-name:${env.BUILD_ID}")
                }
            }
        }
        stage('Deploy Container') {
            steps {
                script {
                    // Docker 컨테이너 실행
                    docker.run("--name your-app-container -d -p 8080:8080 your-app-name:${env.BUILD_ID}")
                }
            }
        }
    }
}
```


