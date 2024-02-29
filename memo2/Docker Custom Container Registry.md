https://novemberde.github.io/post/2017/04/09/Docker_Registry_0/


# Docker registry 구축



**docker registry 의 기본포트는 5000번**
```shell
# registry 이미지 가져오기
docker pull registry
```
```shell
# registry 실행
 docker run -dit --name docker-registry -p 5000:5000 registry
```

---

# Docker 이미지를 Push 하기

Docker Hub 사용 시 : <계정 아이디>/registry:latest -> tag 명에 본인 ID 가 들어감.

private registry 사용 시 : <계정 아이디> 부분에 registry 의 url 이 들어감.

```shell
docker pull hello-world

docker tag hello-world localhost:5000/hello-world
```

registry 에 push
```shell
# 이미지 push 
docker push localhost:5000/hello-world

# 이미지 확인
curl -X GET http://localhost:5000/v2/_catalog
# result : {"repositories": ["hello-world"]}

# 태그 정보 확인
curl -X GET http://localhost:5000/v2/hellp-world/tags/list
# result : {"name" : "hello-world", "tag":["latest"]}
```


*  