
## 란?

GitHub Actions 는 빌드, 테스트 및 배포 파이프라인을 자동화 할 수 있는 CI/CD 플랫폼. 리포지토리에 대한 모든 풀 요청을 빌드 및 테스트하거나 병합된 풀 요청을 프로덕션에 배포하는 워크플로우를 생성할 수 있음.



## 구성 요소

PR 요청이 열리거나 ISSUE가 생성되는 등 리포지토리에서 이벤트가 발생할 때
트리거가 되도록 GitHub Actions 워크플로우를 구성할 수 있음.

워크풀로우에는 순차적 또는 병렬로 실행될 수 있는 작업이 하나 이상 포함되어 있음.

각 작업은 자체 가상 머신 러너 안에서 또는 컨테이너 안에서 실행되며, 정의한 스크립트를 실행하거나 액션을 실행하는 하나 이상의 단계를 포함함.

Actions 는 워크플로우를 단순화할 수 있는 재사용 가능한 확장 기능임.

1. 워크플로우
	* 하나 이상의 작업을 포함하며, 특정 이벤트에 의해 자동으로 실행되도록 설정된 YAML 파일로 구성됨. 워크플로우 파일은 리포지토리의 `.github/workflows` 디렉토리에 위치함.

2. 이벤트(Event)
	* 워크플로우는 GitHub 에서 발생하는 특정 이벤트에 의해 트리거가 됨.
	  예를 들어 `push`, `pull request`, `issues`, `schedule`, `repository_dispatch` 등이 있음.

3. 작업(Job)
	* 워크플로우 내에서 실행되는 일련의 단계를 포함하는 작업 단위. 각 작업은 독립적으로 실행되거나 다른 작업에 의존할 수 있음.

4. 단계(Step)
	* 각 작업은 하나 이상의 단계로 구성됨. 단계는 개별적인 작업이나 쉘 명령을 실행함.

5. Action
	* 재사용 가능한 워크플로우 컴포넌트로, 공개 리포지토리에서 가져오거나 직접 생성할 수 있음. 액션은 특정 작업을 수행하도록 미리 작성된 코드 블록.

**예제**

다음은 `push` 이벤트가 발생할 때 Node.js 애플리케이션을 빌드하고 테스트하는 간단한 워크플로우임.

```yaml
name: Node CI

on: [push]

jobs:
  build:

    runs-on: ubuntu-latest

    strategy:
      matrix:
        node-version: [12.x, 14.x, 16.x]

    steps:
    - uses: actions/checkout@v2
    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v2
      with:
        node-version: ${{ matrix.node-version }}
    - run: npm install
    - run: npm test
      env:
        CI: true
```


## 특징

1. 플랫폼 독립성
	* GitHub Actions 는 Linux, macOS, Windows 를 지원하므로 다양한 환경에서 작업을 실행할 수 있음.

2. 언어 및 프레임워크 독립성
	* 어떤 프로그래밍 언어나 프레임워크를 사용하든 GitHub Actions 와 함께 사용할 수 있음.

3. 사용자의 정의 워크플로우
	* 사용자가 필요에 따라 워크플로우를 자유롭게 정의하고 구성할 수 있음.

4. 마켓플레이스 통합
	* GitHub 마켓플레이스에서 수많은 준비된 Actions 를 찾아서 사용할 수 있으며, 커뮤니티가 만든 Actions 도 사용할 수 있음.
