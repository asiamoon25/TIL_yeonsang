## Docker란?

**컨테이너 기반의 오픈소스 가상화 플랫폼**

### container 란?
**[container](obsidian://open?vault=TIL_yeonsang&file=TIL%2FContainer%2FContainer)**
격리된 공간에서 프로세스가 동작하는 기술, 가상화 기술의 하나 이지만 기존 방식과는 차이가 있음.

**기존**
OS를 가상화했음.
여러가지 OS 를 가상화 할 수 있고 비교적 사용법이 간단하지만 무겁고 느려서 운영환경에선 사용할 수 없다.
위 문제점을 개선하기 위해 **프로세스 격리** 방식이 등장.
리눅스에서는 이 방식을 리눅스 컨테이너라고 하고 단순히 프로세스를 격리시키기 때문에 가볍고 빠르게 동작한다.
CPU나 메모리는 딱 프로세스가 필요한 만큼만 추가로 사용하고 성능적으로도 거의 손실이 없다.

### Image

Docker Image 를 빌드하면 Dockerfile의 매 커맨드마다 실행된 결과(delta)가 레이어로 추가되며, 매 레이어에는 고유한 식별자가 부여된다. 이 레이어는 동일한 문맥 내에서는 동일한 결과를 만들어내기 때문에 캐싱에 용이
변경이 잦은 커맨드는 가능한 뒤에 실행하는 것이 좋다.



### Dockerfile

Dockerfile 은 도커 컨테이너를 생성하는 가장 대표적이고 보편적인 방법

