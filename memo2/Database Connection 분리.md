## DataSourceHelper

변수

dbConnectionInfo ➡️ db 정보 담은 Properties
databaseName ➡️ 실제 DB 에서 사용하는 스키마이름
server ➡️ DB Host
username, password, url
dbDriver ➡️ JDBC 드라이버 이름
dbType ➡️ 어떤 DB 를 사용하는지
dataSourceName ➡️ DataSource.groovy 에서 사용하던 이름 그대로

### BootStrap.groovy

```java
def init = {
	// grails application 동작 시 처음으로 시작되는 부분
	DataSourceHelper.metaClass.methods.each{ MetaMethod mothod ->
		if (method.static && method.returnType == Properties) {  
			Properties dbProps = method.invoke(null) // static 메서드 호출  
			String dataSourceName = dbProps.get("dataSourceName").toString()  
			DynamicConnectionPoolManager.addDbProperties(dataSourceName, dbProps) 
		}
	}
}

def destroy = {  
	DynamicConnectionPoolManager.closeAll()  
}
```


#### DynamicConnectionPoolManager.groovy
1. isConnectionValid
```groovy
private static boolean isConnectionValid(DataSource dataSource, String dbType) {  
	String query = "SELECT 1"  
	if(dbType && dbType == 'oracle'){  
		query = "SELECT 1 FROM DUAL"  
	}  
	try {  
		Connection conn = dataSource.getConnection()  
		Statement stmt = conn.createStatement()  
		stmt.executeQuery(query)  
		conn.close()  
		return true  
	} catch (SQLException e) {  
		return false  
	}  
}
```
validateQuery 를 날려 Connection Pool 을 잡는 곳

2. addDbProperties
```groovy
static void addDbProperties(String dataSourceName, Properties dbProps) {  
	dbPropertiesMap.put(dataSourceName, dbProps)  
}
```
BootStrap.groovy 에서 grails 시작 시 initialize 하기 위한 메서드