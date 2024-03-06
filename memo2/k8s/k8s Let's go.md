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

### JENKINS 에서 Docker 이미지 빌드 및 배포 자동화

1. Jenkins 에 Docker 플러그인 설치: Jenkins 관리 페이지에서 플러그인 관리를 통해 Docker Plugin 을 설치
2. 빌드 스크립트 작성
```sh
# 이미지 빌드
docker build -t HAPPYCODE:test .

# Docker 이미지를 Docker hub 나 다른 registry 에 push -> Azure Registry
docker push HAPPYCODE:test

# 추가적인 배포 스크립트(k8s 클러스터에 배포)
kubectl set image deployment/your-app-deployment
```