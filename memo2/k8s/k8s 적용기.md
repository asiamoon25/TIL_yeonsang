# 1. 백엔드 애플리케이션 컨테이너화

1. Dockerfile 작성
	애플리케이션을 위한 Dockerfile 작성. war 파일을 tomcat 서버나 다른 서블릿 컨테이너에 배포하는 과정을 자동화 함.
```dockerfile
FROM tomcat:9.0
COPY ./path/to/your-app.war /usr/local/tomcat9/webapps/your-app.war
EXPOSE 8080
CMD ["catalina.sh", "run"]
```

2. 이미지 빌드
	Dockerfile 이 있는 디렉토리에서 명령어를 사용하여 Docker 이미지를 빌드
```bash
docker build -t your-backend-app:tag .
```

# 2. 쿠버네티스에서 백엔드 애플리케이션 배포
1. Deployment 생성
	백엔드 애플리케이션을 실행하기 위한 k8s Deployment 를 생성
예시)
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
	name: your-backend-app
spec:
	replicas: 2 # 초기 복제본 수
	selector:
		matchLabels:
			app: your-backend-app
	template:
		metadata:
			labels:
				app: your-backend-app
		spec:
			containers:
			 - name: your-backend-app
			   image: your-backend-app:tag
			   ports:
			   - containerPort: 8080
```