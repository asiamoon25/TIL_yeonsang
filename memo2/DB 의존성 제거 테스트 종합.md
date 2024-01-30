## 개요

#### 목적
Connection Pool 제거 후 데이터베이스 성능과 안정성 평가.

#### 중점 사항
Connection Pool 제거 후 테스트를 하면서 성능 저하 및 시스템 안정성에 어떤 영향을 미치는지 분석

#### 테스트 환경
* 테스트 도구 : Jmeter, Terminus(모니터링), Azure Portal 
* 사용된 데이터베이스 : MySQL
* 서버 정보 
	* IP : 10.100.100.5
	* CPU : 2core
	* MEM: 8GB

## 테스트 방법

#### 구성

* connection pool 제거
```java
public static Properties getAuditionConnectionInfo() {  
Properties dbConnectionInfo = new Properties()  
String databaseName = ""  
String server = ""  
if(Environment.current == Environment.TEST){  
databaseName = "audition"  
server = "10.4.11.3"  
dbConnectionInfo.put("password","happycode")  
}else {  
databaseName = "audition"  
server = "10.4.11.16"  
dbConnectionInfo.put("password","jcej0j;3!@#")  
}  
dbConnectionInfo.put("url","jdbc:mysql://"+server+":3306/"+databaseName+"?autoreconnect=true&useUnicode=yes&characterEncoding=latin1&character_set_server=latin1")  
dbConnectionInfo.put("username","happycode")  
dbConnectionInfo.put("databaseName",databaseName)  
dbConnectionInfo.put("dataSource","mysql")  
return dbConnectionInfo  
}
```