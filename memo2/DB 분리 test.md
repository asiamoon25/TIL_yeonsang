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
![[Pasted image 20240122163214.png]]



-----
TEST (DBConnection 분리 적용)





reward point use history