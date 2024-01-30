시간 : 11:00 ~ 완료 후 회신

내용 :  DB Connection Pool 제거 부하 테스트

호출하는 API : gsApi/checkExistIngameAccount

호출 가는 DB : GERSANGACCOUNT(10.4.7.4)

사용하는 쿼리 : 
```sql
DECLARE @return_value int,  
@result tinyint  
EXEC @return_value = [dbo].[JOY_CheckOnlyID]  
@id = N'%s',  
@result = @result OUTPUT  
SELECT @result as N'result'
```

Connection 확인 한 쿼리
```sql
SHOW STATUS LIKE 'Threads_connected';
```

------

TEST (DB Connection 분리 미적용)
현재 Connection 수 (QA Audition DB)
![[Pasted image 20240123111301.png]]
1만건 요청 시
![[Pasted image 20240123111313.png]]

시간 : 1분

-----
TEST (DBConnection 분리 적용)

![[Pasted image 20240123111558.png]]

1만건 요청 시
![[Pasted image 20240123112355.png]]

6분


-----


DB Connection Pool 을 startup 완료 후 잡을 때
![[Pasted image 20240123170729.png]]


![[Pasted image 20240123170939.png]]
1분 16초


----------------

기존 QA
2분
![[Pasted image 20240129115434.png]]

![[Pasted image 20240129115638.png]]




Conneciton Pool 분리한 소스
1분 30초
![[Pasted image 20240129115653.png]]

![[Pasted image 20240129115638.png]]




