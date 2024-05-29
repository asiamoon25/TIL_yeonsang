---
sticker: emoji//0031-fe0f-20e3
---
## 테이블 설계
_아... 처음부터 하기 싫음.._

### 사용할 데이터 수급처

**공공데이터**
↪️ 쓸만한 곳이 여기 밖에 없음.. 말 관련된거는 다 찾아야됨.



1. 경주 성적 정보 [여기서](https://www.data.go.kr/tcs/dss/selectApiDataDetailView.do?publicDataPk=15063979)
	* 통계 용
3. 경주기록 정보 [여기서](https://www.data.go.kr/tcs/dss/selectApiDataDetailView.do?publicDataPk=15058305)
	* 통계 용
4. 경주 계획표 [여기서](https://www.data.go.kr/tcs/dss/selectApiDataDetailView.do?publicDataPk=15056499)
	* 일정 알림페이지?
5. 확정 배당율 [여기서](https://www.data.go.kr/tcs/dss/selectApiDataDetailView.do?publicDataPk=15057896)
	* 통계 용
6. 경주마 성적정보 [여기서](https://www.data.go.kr/tcs/dss/selectApiDataDetailView.do?publicDataPk=15058779)
	* 말 개인 통계
7. 마필 종합 상세정보 [여기서](https://www.data.go.kr/tcs/dss/selectApiDataDetailView.do?publicDataPk=15057985)
	* 말 개인 정보 확인 용


깡데이터들이여서 DB에 적재해야함. -> 데이터 타입 다 파악해서 적절한 타입으로 정리해서 넣어야함. ➡️ 한번 씩 다 호출하고 해야함...

**Index** 넣어야 할거

1. 말 번호
2. meet? 경기장 정보
3. 부모말

테이블 일단 쪼개지 말고 데이터 다 넣은 후 확인.



## 통계 내야할 것들

1. 승률 통계
	* 각 경주마의 승률, 입상률
	* 조교사와 기수의 승률

2. 경기장별 성적
	* 경기장의 특성에 따라 달라짐(흙, 잔디, 거리, 날씨 등) 에 따라 성적이 크게 달라질 수 있으므로 경기장별로 경주마의 성적을 분석하여 특정 경기장에서 강한 말을 파악할 수 있음.

3. 연령별, 성별 성적 분석
	* 경주마의 연령과 성별에 따른 성적을 분석하여, 특정 연령대나 성별의 말이 우수한 성적을 내는 경향이 있는지 조사

4. 시간대별 성적 변화
	* 일정 시간대(예: 오전,오후,저녁) 에 따른 말의 성적을 분석하여, 특정 시간대에 강한 경주마를 파악할 수 있음.

5. 배당률과 실제 입상률 비교
	* 배당률이 높은 말과 실제 입상률을 비교하여, 배당률이 경주마의 실제 성적을 얼마나 정확하게 반영하는지 분석할 수 있음.

6. 복승식, 쌍승식 배팅 데이터 분석
	* 두 마리의 말을 선택하여 입상을 예측하는 복승식이나 쌍승식 베팅에서, 자주 선택되는 말의 조합과 실제 입상 결과를 비교 분석

7. 경주 전후 데이터 비교
	* 경주 전후의 말의 컨디션, 훈련 데이터 등을 비교하여 경주 결과에 어떤 요소가 가장 큰 영향을 미쳤는지 분석할 수 있음.

