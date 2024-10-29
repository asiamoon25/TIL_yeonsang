
## 란?

* Go 언어로 작성된 리눅스 Container 기반으로하는 오픈소스 가상화 플랫폼
* Docker 0.9 버전 부터는 직접 개발한 libcontainer 컨테이너를 사용하고 있음.


## 왜 사용함?

1. 일관성 있는 개발 환경
	* 개발, 테스트, 프로덕션 환경에서 동일한 설정을 유지할 수 있음.

2. 이식성
	* 컨테이너는 어디서나 동일하게 실행되므로 환경에 영향을 받지 않음.

3. 효율성 
	* 시스템 자원을 효율적으로 사용할 수 있으며, 컨테이너는 VM 보다 가볍고 빠르게 배포할 수 있음.

4. 확장성
	* 컨테이너 기반 아키텍쳐는 수평적 확장이 용이하며, 클러스터링 도와 결합하여 쉽게 확장할 수 있음.

5. 격리
	* 각 컨테이너는 독립된 환경을 제공하여 애플리케이션 간의 종속성 충돌을 방지함.


## Docker 까보기

1. Image
	* Application 과 모든 종속성을 포함하는 읽기 전용 템플릿임. Dockerfile 을 사용하여 생성됨.

2. Container
	* 이미지를 실행한 상태로, 애플리케이션이 동작하는 환경을 제공함.

3. Dockerfile
	* 이미지를 빌드하기 위한 명령어를 포함하는 텍스트 파일

4. Docker Hub
	* Docker 이미지를 공유하고 저장하는 중앙 저장소



## 사용법

Docker 는 Window, macOS, Linux 에서 사용할 수 있음. 공식 사이트에서 설치 프로그램을 다운로드 하여 설치하면 됨.

Window 는 BIOS 에서 Hyper-V 옵션이 켜져있는지 확인해야함.



## 기본 명령어

1. 이미지 검색 및 다운로드

```bash
docker pull <image-name>
```

ex) `docker pull nginx`


2. 컨테이너 실행

```bash
docker run -d -p <hostPort>:<containerPort> <image-name>
```

hostPort : 컴퓨터 호스트
containerPort : 컨테이너 내부 호스트

ex) `docker run -d -p 80:80 nginx`

3. 실행 중인 컨테이너 목록 보기

```bash
docker ps
```

4. 컨테이너 정지

```bash
docker stop <Container ID>
```

5. 이미지 목록 보기

```bash
docker image
```

6. 이미지 삭제

```bash
docker rmi <Image ID>
```


## Dockerfile 작성 및 이미지 빌드

1. Dockerfile 작성

```Dockerfile
# base image setting
FROM ubuntu:latest

# 필요한 패키지 설치
RUN apt-get update && apt-get install -y python3

# 애플리케이션 복사
COPY . /app

# 작업 디렉토리 설정
WORKDIR /app

# 애플리케이션 실행 명령어 설정
CMD ["python3", "app.py"]
```

2. image build

```bash
docker build -t <image-name>
```

ex) `docker build -t my-python-app`

3. image 로 컨테이너 실행

```bash
docker run -d -p 5000:5000 my-python-app
```


## Docker Compose 사용

Docker Compose 는 다중 컨테이너 애플리케이션을 정의하고 실행하기 위한 도구

1. docker-compose.yml 작성

```yml
version: '3'
services:
	web:
		image: nginx
		ports:
			- "80:80"
	app:
		build: .
		ports:
			- "5000:5000"
```

2. Compose 로 애플리케이션 실행

```bash
docker-compose up
```

3. Compose 로 애플리케이션 중지

```bash
docker-compose down
```

