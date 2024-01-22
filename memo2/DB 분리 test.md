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



------

TEST 전
현재 Connection 수
![[Pasted image 20240122111635.png]]



-----
TEST 후
