## Container란?

컨테이너는 어떤 환경에서나 실행하기 위해 필요한 모든 요소를 포함하는 소프트웨어 패키지

컨테이너는 소프트웨어 서비스를 실행하는 데 필요한 특정 버전의 프로그래밍 언어 런타임 및 라이브러리와 같은 종속 항목과 애플리케이션 코드를 함께 포함하는 경량 패키지

애플리케이션을 환경에 구애 받지 않고 실행하는 기술

## 기존 VM 과의 차이

VM은 하드웨어 엑세스 권한을 갖는 호스트 운영체제 위에서 리눅스나 윈도우 같은 게스트 운영체제를 실행하는 개념 (운영체제 위의 운영체제)

Container 는 운영체제 위에 Docker 같은 엔진을 두고, 이를 통해 가상화된 패키지를 올림.
![[Pasted image 20231012143505.png]]

### Container 특징
1. 높은 이식성
2. VM 과 비교했을 때 훨씬 적은 자원을 소비
3. 빠른 속도와 효율성
4. 상태를 가지지 않음 (Stateless)

**높은 이식성**
Container는 호스트 환경이 아닌 독자적인 실행 환경을 가지고 있음.

**VM 과 비교했을 때 훨씬 적은 자원을 소비**
구동에 필요한 Guest OS 가 사라지고 Container Engine 위에서 돌아가기 때문에 OS 구동 시킬 필요도 없고 OS 구동에 들어갈 자원들이 없어진다. 그리고 application  구동에 필요한 Guest OS 또한 필요 없기 때문에 GB 정도의 용량에서 MB 까지 줄어들 수 있다.

**빠른 속도와 효율성**
적은 자원을 소비한다는 부분과 동일하게 Guest OS 를 구동시킬 필요가 없기 때문에 들어가는 메모리 등 다른 자원이 쓰일 일이 없이 내 환경에 맞춘 application 을 구동하기 때문에 더 빠른 속도를 가질 수 있다.

**상태를 가지지 않음**
컨테이너가 실행되는 환경은 독립적이기 때문에, 다른 컨테이너에게 영향을 주지 않음. Docker 와 같이 이미지 기반으로 Container를 실행하는 경우 특정 실행 환경을 쉽게 재사용 할 수 있음.

### 이점

* 가벼움
* 탄력성
* 유지 관리 효율

**가벼움**
	위에 나온 Container 특징에서 VM 보다 훨씬 적은 자원을 소비함.
	기존 VM은 GB 정도라면 Container 는 MB 정도 이다.
	이러한 이유는 Container 에는 apllication을 실행하는데 필요한 라이브러리와 설정만 가지고 있기 때문

**탄력성**
	컨테이너는 Linux, Windows, 가상머신, Data Center, Public Cloud 등 어느 환경에서나 구동이 됨.

**유지 관리 효율**
	운영 체제 커널이 하나밖에 없기 때문에 운영 체제 수준에서 업데이트 또는 패치 작업을 한 번만 수행하면 변경 사항이 모든 컨테이너에 적용됨.

### 단점

* 보안 이슈
	Container 는 Kernel 을 공유함. 논리적인 격리 개념으로 보면 되는데 물리적으로 격리한 가상머신에 비해서는 보안이 취약하다.
