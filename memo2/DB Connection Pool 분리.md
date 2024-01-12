test 툴 : jmeter
사용한 메서드 checkExistInGameAccount (gs)
요청 request : 10만건
사용한 쓰레드 개수 : 10개
쓰레드당 보낸 요청 : 1만건
10.100.100.5 top
![[Pasted image 20240111171733.png]]

DB CPU
![[Pasted image 20240111171841.png]]
DB IO
![[Pasted image 20240111173339.png]]

10.100.100.5
![[Pasted image 20240111172124.png]]


----

GS DATASOURCE 분리 했을 때.......!!!!!!!
branch/yeonsang/DB_DEPENDENCY_DELETE

test 툴 : jmeter
사용한 메서드 checkExistInGameAccount (gs)
요청 request : 10만건
사용한 쓰레드 개수 : 10개
쓰레드당 보낸 요청 : 1만건

![[Pasted image 20240111172924.png]]

DB CPU
![[Pasted image 20240111173107.png]]

10.100.100.5 
![[Pasted image 20240111173028.png]]

DB IO
![[Pasted image 20240111173210.png]]



비교
CPU 차이
10.100.100.5 서버
![[Pasted image 20240111173735.png]]

DB 서버
![[Pasted image 20240111173857.png]]
DB IO, CPU 차이


-----
01-12
정상
![[Pasted image 20240112095026.png]]

![[Pasted image 20240112095207.png]]


GS DB Connection 제거
09:54 시작 ~ 10:01
sql-happycode  CPU
![[Pasted image 20240112100225.png]]

qa server 
![[Pasted image 20240112100325.png]]
평균 : 5% -> 26% 증가

IO 평균 813kb -> 18mb 증가
![[Pasted image 20240112100443.png]]

VM 가용 메모리
평균 190MB -> 169MB 하락
![[Pasted image 20240112100551.png]]


GS DB Connection 연결된 상태
시작 시간 10:11 ~ 

DB 
![[Pasted image 20240112101850.png]]

IO
![[Pasted image 20240112101929.png]]

