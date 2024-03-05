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

2. Deployment:
```shell
kubectl apply -f backend-deployment.yaml
```


# 3. 오토 스케일링 설정
1. Horizontal Pod Autoscaler(HPA) 생성 : 트래픽이 많아질 때 백엔드 애플리케이션의 복제본 수를 자동으로 늘릴 수 있도록 HPA 를 설정함.
	HPA 예시 명령어
```shell
kubectl autoscale deployment your-backend-app --min=2 --max=10 --cpu-percent=80
```
이 명령어는 CPU 가 80퍼센트 를 초과하면 자동으로 복제본 수를 늘리고, 최소 2개에서 최대 10개까지 복제본을 유지하도록 설정함.


# 추가 고려 사항
- **서비스(Service) 생성**: 백엔드 애플리케이션에 외부 또는 내부 네트워크에서 접근하기 위해 쿠버네티스 서비스를 생성해야 함
- **보안 및 환경 설정**: 쿠버네티스에서 애플리케이션을 실행할 때 보안, 환경 변수, 비밀번호 등의 설정을 고려해야 한다.
- **로그 및 모니터링**: 쿠버네티스에서는 애플리케이션 로그 및 모니터링을 위한 다양한 도구와 통합 옵션을 제공한다.



Azure 에서 제공하는 AKS (Azure Kubernetes)

