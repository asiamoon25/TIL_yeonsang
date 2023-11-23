url : /Index/Billing/MyCard/Payment

jcgf_qa 에서 any_point 리스트 조회

paymetnt.jsp 에 보여질 때 게임 리스트는 
game.gameStatus.name eq 'OPEN_BETA' || game.gameStatus.name eq 'SERVICE_NORMAL' || game.gameStatus.name eq 'SERVICE_PORTAL' 일때만

**게임 선택 후**
1,3 번째 선택 시
/mycardv25/api/billing/getProducts.json 으로 충전 가격 정해줌

2번 선택 시 
원하는 금액 입력


**충전 마지막**
/mycardv25/api/billing/startCharge.json 