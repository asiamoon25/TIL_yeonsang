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



Azure 클라우드에서 프론트엔드 VM(가상 머신)과 백엔드 쿠버네티스(Kubernetes, K8s) 클러스터를 연결하는 일반적인 방법은 네트워크 리소스와 서비스를 사용하는 것입니다. 이 연결 과정은 보안, 확장성, 그리고 관리 효율성을 고려해야 함.

### 1. Azure Load Balancer 사용

Azure Load Balancer를 사용하여 프론트엔드 VM과 백엔드 K8s 서비스 간의 트래픽을 관리할 수 있습니다. 이 방법은 고가용성, 자동 스케일링, 그리고 안정적인 트래픽 분산을 제공한다.

1. **백엔드 Kubernetes 서비스 생성**: 백엔드 애플리케이션을 위한 K8s 서비스를 `LoadBalancer` 타입으로 생성합니다. 이 서비스는 Azure의 로드 밸런서에 자동으로 연결되며, 외부 IP 주소를 할당받는다.
    
2. **프론트엔드 VM 구성**: 프론트엔드 애플리케이션은 백엔드 서비스의 외부 IP 주소(또는 DNS 이름)를 사용하여 백엔드 K8s 클러스터에 연결합니다. 이 IP 주소는 백엔드 서비스를 생성할 때 할당되며, `kubectl get services` 명령어로 확인할 수 있다.
    
3. **보안 그룹 설정**: Azure에서는 네트워크 보안 그룹(NSG)을 사용하여 특정 포트로의 인바운드 및 아웃바운드 트래픽을 제어할 수 있다. 프론트엔드 VM과 백엔드 K8s 서비스 간의 통신을 허용하려면, 적절한 NSG 규칙을 구성해야 한다.
    

### 2. Azure Virtual Network 통합

Azure Virtual Network(VNet)를 사용하여 프론트엔드 VM과 백엔드 K8s 클러스터 간의 안전한 연결을 구성할 수 있습니다. 이 방법은 두 환경 간의 네트워크 격리를 제공하면서도, 서로 간에 안전하게 통신할 수 있게 한다.

1. **VNet 피어링**: 프론트엔드 VM이 위치한 VNet과 백엔드 K8s 클러스터가 위치한 VNet 간에 VNet 피어링을 설정한다. 이를 통해 두 VNet 간의 안전한 네트워크 통신 경로를 구성할 수 있다.
    
2. **Private Link 또는 Private Endpoint 사용**: 백엔드 K8s 서비스에 대해 Azure Private Link를 사용하여, 프론트엔드 VM이 백엔드 서비스에 대해 프라이빗 네트워크를 통해서만 접근할 수 있도록 설정할 수 있다. 이는 데이터가 공용 인터넷을 거치지 않고 Azure의 백본 네트워크 내에서만 전송되도록 보장한다.
    
3. **DNS 설정**: 프론트엔드 VM에서 백엔드 K8s 서비스에 접근할 때, DNS 이름을 사용하여 연결할 수 있도록 Azure DNS를 구성할 수 있다. 이를 통해 백엔드 서비스의 IP 주소가 변경되더라도 프론트엔드 애플리케이션이 계속해서 백엔드 서비스에 접근할 수 있게 된다.
    

### 보안 및 모니터링

- **NSG 및 방화벽 규칙**: VM과 K8s 클러스터 간의 통신을 보호하기 위해 적절한 네트워크 보안 그룹(NSG)과 Azure 방화벽 규칙을 구성한다.
- **Azure Monitor 및 Azure Security Center**: 애플리케이션과 네트워크의 성능 및 보안 상태를 모니터링하기 위해 Azure Monitor와 Azure Security Center를 활용할 수 있다.

이러한 구성을 통해 Azure 클라우드에서 프론트엔드 VM과 백엔드 K8s 클러스터를 효과적으로 연결하고, 고가용성 및 보안을 유지할 수 있다.










---





로컬 환경에서 프론트엔드와 백엔드(쿠버네티스 클러스터 내)를 연결하는 것은 클라우드 환경에서와는 다르게 진행됩니다. 로컬에서는 주로 개발 및 테스트 목적으로 설정을 구성하며, 이를 위해 몇 가지 다른 접근 방식을 사용할 수 있습니다.

### 1. `kubectl port-forward` 사용

로컬 개발 중에는 `kubectl port-forward` 명령을 사용하여, 로컬 머신에서 쿠버네티스 클러스터 내의 특정 서비스나 파드에 직접 접근할 수 있습니다. 이 방법은 빠르게 백엔드 서비스에 연결하고 테스트하기 위한 간단한 솔루션을 제공합니다.

예를 들어, 백엔드 서비스가 쿠버네티스 클러스터 내에서 `8080` 포트에서 실행 중이라고 가정해 보겠습니다. 로컬 머신의 `8081` 포트를 통해 이 서비스에 접근하려면 다음 명령을 사용할 수 있습니다:

shCopy code

`kubectl port-forward service/your-backend-service 8081:8080`

이 명령은 로컬 머신의 `8081` 포트와 쿠버네티스 서비스의 `8080` 포트 사이에 포워딩을 설정합니다. 이제 브라우저나 다른 클라이언트에서 `http://localhost:8081`을 통해 백엔드 서비스에 접근할 수 있습니다.

### 2. Ingress 컨트롤러 사용

로컬 쿠버네티스 클러스터에서 Ingress 컨트롤러를 사용하여 HTTP/HTTPS 트래픽을 백엔드 서비스로 라우팅할 수 있습니다. Minikube, kind, 또는 Docker Desktop과 같은 도구를 사용하여 로컬에서 쿠버네티스 클러스터를 실행할 경우, Ingress 컨트롤러를 설정하여 사용할 수 있습니다.

예를 들어, Minikube를 사용하는 경우, Ingress 컨트롤러를 활성화하기 위해 다음 명령을 실행할 수 있습니다:

shCopy code

`minikube addons enable ingress`

Ingress 리소스를 정의하여 특정 호스트 이름을 사용하여 로컬에서 백엔드 서비스에 접근할 수 있게 설정할 수 있습니다. 예를 들어, `backend.local` 호스트 이름을 사용하여 로컬의 백엔드 서비스에 접근하도록 구성할 수 있습니다.

### 3. 로컬 네트워크 설정

로컬 개발 환경에서 프론트엔드와 백엔드 서비스 간의 연결을 테스트하기 위해, 프론트엔드 애플리케이션의 네트워크 요청을 백엔드 서비스의 로컬 또는 리모트 주소로 직접 지정할 수 있습니다. 개발 중인 프론트엔드 애플리케이션의 설정 파일에서 백엔드 서비스의 주소를 `http://localhost:8081`과 같이 지정하여 이를 달성할 수 있습니다.

### 4. 환경 변수 사용

환경 변수를 사용하여 백엔드 서비스의 URL을 프론트엔드 애플리케이션에 제공하는 것도 좋은 방법입니다. 이 방법은 프론트엔드 애플리케이션의 코드를 변경하지 않고도 다양한 환경(개발, 테스트, 프로덕션)에서 백엔드 서비스의 URL을 유연하게 설정할 수 있게 해줍니다.

로컬 개발 환경 설정은 주로 개발 편의성과 빠른 테스트를 목적으로 하므로, 보안이나 프로덕션 환경에서의 고가용성과 같은 요소는 덜 중요할 수 있습니다. 그러나 로컬에서 설정한 연결 방식이 실제 클라우드 환경에서도 잘 동작하는지 확인하는 것이 중요합니다.