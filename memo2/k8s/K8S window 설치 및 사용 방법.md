# window

wsl2 로 kind 설치 해서 하면 된다.

### kind 란?
Kubernetes In Docker 의 약자
Docker 에서 쿠버네티스를 할 수 있게 해줌.

### wsl 에서 하는 법 

```powershell
> wsl
```

```shell
$ curl -Lo ./kind https://github.com/kubernetes-sigs/kind/releases/download/v0.10.0/kind-linux-amd64 --insecure
```

o 옵션을 써서 파일로 들어오게 된다.
```shell
chmod -x ./kind
```

전역 사용을 위한 mv
```shell
sudo mv ./kind /usr/local/bin
```



### Kubernetes Cluster 생성

[쿠버네티스에서 사용되는 기능게이트](obsidian://open?vault=TIL_yeonsang&file=memo2%2Fk8s%2Fk8s%20%EA%B8%B0%EB%8A%A5%EA%B2%8C%EC%9D%B4%ED%8A%B8)

1. yml 작성
```yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4  ===> v1alpha4 임을 지정
name: app-1-cluster    -> 클러스터 이름 지정


```