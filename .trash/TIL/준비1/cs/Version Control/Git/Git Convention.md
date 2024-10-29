

## 란?

* Git 커밋 메시지 규칙은 코드 변경 사항을 명확하게 설명하고 협업을 원활하게 하기 위한 표준임.


## 규칙


1. 제목(Subject)
	* 형식 : `type(scope): subject`
	* 예시 : `feat(auth): add login functionality`
	* 종류
		* feat : 새로운 기능 추가
		* fix : 버그 수정
		* docs : 문서 변경
		* style : 코드 포맷팅, 세미콜론 누락 등(비즈니스 로직에 변경 없음)
		* refactor : 코드 리팩토링
		* test : 테스트 추가 및 수정
		* chore : 빌드 작업 업데이트, 패키지 매니저 설정 등

2. 본문 (Body)
	* 형식 : 제목과 본문은 빈 줄로 구분
	* 내용 : 변경 이유와 방법을 설명
**예시**
```text
feat(auth): add login functionality

- add login API endpoint
- intergrate JWT for authentication
- update frontedn to handle login state
```


3. 꼬리말(Footer)
	* 형식 : 해결된 이슈와 참고사항 추가
	* 내용:
		* `Closes #123` : 이슈 닫기
		* `BREAKING CHANGE` : 코드 변경으로 인해 호환성이 깨지는 경우
**예시**
```text
Closes #123
```


**최종 예시**
```text
feat(auth): add login functionality

- add login API endpoint
- integrate JWT for authentication
- update frontend to handle login state

Closes #123
```



### 추가적인 규칙
* 대소문자 : 제목은 소문자로 시작, 마지막에 마침표 생략
* 길이 제한 : 제목은 50자 이내, 본문은 72자 줄바꿈

### 이슈번호 관리
* 이슈 번호 부여 : GitHub, GitLab 등에서 이슈를 생성하면 자동으로 번호가 부여
* 이슈 참조 : 커밋 메시지에서 이슈 번호를 참조하여 관련성을 유지



