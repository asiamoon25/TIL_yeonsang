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
[쿠버네티스에서 사용되는 kube-apiserver](https://kubernetes.io/docs/reference/command-line-tools-reference/kube-apiserver/)
## <span style="color:red">클러스터 공개하기전에 3번 이상 생각하기</span>
1. yml 작성
```yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4  ===> v1alpha4 임을 지정
name: app-1-cluster    -> 클러스터 이름 지정
featureGates:
     # 넣고 싶은 기능 게이트들 넣기
     "CSIMigration": true
runtimeConfig:
     "api/alpha": "false"
#Windows 또는 Mac에서 Docker를 사용하는 경우 IPv6 포트 전달이 이러한 플랫폼에서 작동하지 않기 때문에 호스트에서 API 서버에 대해 IPv4 포트 전달을 사용해야함. 
networking:
     ipFamily: ipv6
     apiServerAddress: "127.0.0.1"
     apiServerPort: 6443
```




