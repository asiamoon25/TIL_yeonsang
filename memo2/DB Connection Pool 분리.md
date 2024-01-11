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