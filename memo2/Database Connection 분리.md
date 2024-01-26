```plantuml
@startuml

actor GrailsApplication

participant BootStrap

participant DataSourceHelper

participant DynamicConnectionPoolManager

participant gameQueryExecuteRowConnectionPool

participant DataSource

  

== Initialization ==

GrailsApplication -> BootStrap: init()

activate BootStrap
BootStrap -> DataSourceHelper: metaClass.methods.each
activate DataSourceHelper
DataSourceHelper --> BootStrap: [Properties for each dataSource]
deactivate DataSourceHelper
BootStrap -> DynamicConnectionPoolManager: addDbProperties(dbName, dbProps)
activate DynamicConnectionPoolManager
DynamicConnectionPoolManager --> BootStrap: void
deactivate DynamicConnectionPoolManager
deactivate BootStrap
== Query Execution ==
GrailsApplication -> gameQueryExecuteRowConnectionPool: executeQuery(dbName, query)
activate gameQueryExecuteRowConnectionPool
gameQueryExecuteRowConnectionPool -> DynamicConnectionPoolManager: getDataSource(dbName)
activate DynamicConnectionPoolManager
DynamicConnectionPoolManager -> DataSource: new DataSource(PoolProperties)
activate DataSource
DataSource --> DynamicConnectionPoolManager: dataSourceInstance
deactivate DataSource
DynamicConnectionPoolManager --> gameQueryExecuteRowConnectionPool: dataSourceInstance
deactivate DynamicConnectionPoolManager
gameQueryExecuteRowConnectionPool -> DataSource: getConnection()
activate DataSource
DataSource --> gameQueryExecuteRowConnectionPool: connection
deactivate DataSource
gameQueryExecuteRowConnectionPool -> connection: execute(query)
activate connection
connection --> gameQueryExecuteRowConnectionPool: queryResult
deactivate connection
gameQueryExecuteRowConnectionPool --> GrailsApplication: queryResult
deactivate gameQueryExecuteRowConnectionPool
@enduml
```


```plantuml
participant BootStrap
participant DataSourceHelper
participant DynamicConnectionPoolManager
== Initialization ==
GrailsApplication -> BootStrap: init()
activate BootStrap
BootStrap -> DataSourceHelper: metaClass.methods.each
activate DataSourceHelper
DataSourceHelper --> BootStrap: [Properties for each dataSource]
deactivate DataSourceHelper
BootStrap -> DynamicConnectionPoolManager: addDbProperties(dbName, dbProps)
activate DynamicConnectionPoolManager
DynamicConnectionPoolManager --> BootStrap: void
deactivate DynamicConnectionPoolManager
deactivate BootStrap
```

![[Pasted image 20240125112108.png]]



```plantuml
actor GrailsApplication
participant BootStrap
participant DataSourceHelper
participant DynamicConnectionPoolManager
participant CommonGameService
participant DataSource
== Query Execution ==
GrailsApplication -> CommonGameService: executeQuery(dbName, query)
activate gameQueryExecuteRowConnectionPool
CommonGameService -> DynamicConnectionPoolManager: getDataSource(dbName)
activate DynamicConnectionPoolManager
DynamicConnectionPoolManager -> DataSource: new DataSource(PoolProperties)
activate DataSource
DataSource --> DynamicConnectionPoolManager: dataSourceInstance
deactivate DataSource
DynamicConnectionPoolManager --> CommonGameService: dataSourceInstance
deactivate DynamicConnectionPoolManager
CommonGameService -> DataSource: getConnection()
activate DataSource
DataSource --> CommonGameService: connection
deactivate DataSource
CommonGameService -> connection: execute(query)
activate connection
connection --> CommonGameService: queryResult
deactivate connection
CommonGameService --> GrailsApplication: queryResult
deactivate CommonGameService
```

TwelveSky2OriginService.groovy
```groovy
String query = String.format(  
"DECLARE @result int exec @result = %s..SP_CountGiftItemSlot '%s' SELECT @result as result"  
,"ACCOUNT2"  
,user.username  
)  
String dataSourceName = 'dataSource_12sky2ori'  
String logPath = 'gameItemSendLog/12sky2OriSlotCheck'  
def result2 = commonGameService.gameQueryExecuteRowConnectionPool(dataSourceName,query, logPath)
```

CommonGameService.groovy
gameQueryExecuteRowConnectionPool
```groovy
def gameQueryExecuteRowConnectionPool(String dataSourceName, String query, String logPath){
        Connection conn = null
        Sql sql = null
        def map = [:]
        try{
            DataSource dataSource = null
//            String dataSourceName = dbInfo.get("dataSourceName").toString() //dataSource_audition
            if(dataSourceName) {
                dataSource = DynamicConnectionPoolManager.getDataSource(dataSourceName)
            }else{
                return map.put('Return',false)
            }
            conn = dataSource.getConnection()
            sql = new Sql(conn)
            if(conn) {
                sql.eachRow(query,
                        {
                            it.getProperties().metaData.each{ obj -> map.put(obj.columnName, it.getAt(obj.columnName))  }
                        }
                )
                if(logPath){
                    String logString = "query: $query, queryResult: $map.toString()"
                    Logger.log3(logString,logPath)
                }
            }
        }catch(Exception e){
            map.put('Return', false)
            String errMsg = e.printStackTrace()
            if(logPath){
                String logString = "query: $query, errMsg: $errMsg"
                Logger.log3(logString,logPath)
            }
        }finally{
            sql?.close()
            conn?.close()
        }
        return map
    }
```


DynamicConnectionPoolManager.groovy
```groovy
    static DataSource getDataSource(String dataSourceName) {
        /*
         dataSource Map 에 db이름에 맞는 datasource 가 있는지 없는지
         또는 dataSource Map 에서 DB 이름에 맞는 dataSource 가 null 로 들어가 있지 않은지
         create 하다가 터지면 dataSource Map 에 null 로 들어감
        */
        if (!dataSources.containsKey(dataSourceName) || dataSources.get(dataSourceName) == null) {
            Properties dbProps = dbPropertiesMap.get(dataSourceName)
            if (dbProps != null) {
                try {
                    DataSource dataSource = createDataSource(dbProps)
                    dataSources.put(dataSourceName, dataSource)
                } catch (Exception e) {
                    dataSources.put(dataSourceName, null) // 실패 시 null로 설정
                    throw new RuntimeException("Failed to create DataSource for $dataSourceName: ${e.message}", e)
                }
            } else {
                throw new IllegalStateException("No database properties found for: $dataSourceName")
            }
        }else {
            // 이미 생성된 DataSource에 대한 유효성 검사
            Properties dbProps = dbPropertiesMap.get(dataSourceName)
            DataSource dataSource = dataSources.get(dataSourceName)
            String dbType = dbProps.get("dbType").toString()
            /*
            Connection 이 있다가 네트워크 문제로 끊겼다가 재연결 될때 Exception 이 나옴.
            create 하다가 터졌을 때 dataSource Map 에서 삭제
            valid 통과 시에는 그냥 넘김
             */
            if (!isConnectionValid(dataSource,dbType)) {
                // 유효하지 않은 경우, DataSource 재생성
                try {
                    dataSource = createDataSource(dbProps)
                    dataSources.put(dataSourceName, dataSource)
                } catch (Exception e) {
                    dataSources.remove(dataSourceName) // 실패 시 DataSource 제거
                    throw new RuntimeException("Failed to recreate DataSource for $dataSourceName: ${e.message}", e)
                }
            }
        }
        return dataSources.get(dataSourceName)
    }
```

---
해당 게임 DB 의 Connection Pool 이 없을 때

DynamicConnectionPoolManager
createDataSource
```groovy
private static DataSource createDataSource(Properties dbProps) {
        PoolProperties p = new PoolProperties()
        String dataSourceName = dbProps.get("dataSourceName") // 실제 사용되는 db 이름
        String dbType = dbProps.get("dbType") // mysql, oracle, postgresql, mssql
        p.setUrl(dbProps.get("url").toString())
        p.setDriverClassName(dbProps.get("dbDriver").toString())
        p.setUsername(dbProps.get("username").toString())
        p.setPassword(dbProps.get("password").toString())
        def connectionProperty =[:]
        if(Environment.current.name == 'test'){
            connectionProperty = dbType == 'oracle'? DataSourceConfig.dbPropertiesForTestOracle.call() : DataSourceConfig.dbPropertiesForTest.call()
        }else if (Environment.current.name == 'production') {
            connectionProperty = dbType == 'oracle'? DataSourceConfig.dbPropertiesForLiveOracle.call() : DataSourceConfig.dbPropertiesForLive.call()
        }
        if(!connectionProperty.isEmpty()){
            p.setJmxEnabled((Boolean)connectionProperty.get("jmxEnabled"))
            p.setInitialSize(connectionProperty.get("initialSize").toString().toInteger())
            p.setMaxActive(connectionProperty.get("maxActive").toString().toInteger())
            p.setMinIdle(connectionProperty.get("minIdle").toString().toInteger())
            p.setMaxIdle(connectionProperty.get("maxIdle").toString().toInteger())
            p.setMaxWait(connectionProperty.get("maxWait").toString().toInteger())
            p.setMaxAge(connectionProperty.get("maxAge").toString().toInteger())
          p.setTimeBetweenEvictionRunsMillis(connectionProperty.get("timeBetweenEvictionRunsMillis").toString().toInteger())
           p.setMinEvictableIdleTimeMillis(connectionProperty.get("minEvictableIdleTimeMillis").toString().toInteger())
            p.setValidationQuery(connectionProperty.get("validationQuery").toString())
           p.setValidationQueryTimeout(connectionProperty.get("validationQueryTimeout").toString().toInteger())
            p.setValidationInterval(connectionProperty.get("validationInterval").toString().toInteger())
            p.setTestOnBorrow((Boolean)connectionProperty.get("testOnBorrow"))
            p.setTestWhileIdle((Boolean)connectionProperty.get("testWhileIdle"))
            p.setTestOnReturn((Boolean)connectionProperty.get("testOnReturn"))
            p.setJdbcInterceptors(connectionProperty.get("jdbcInterceptors").toString())
       p.setDefaultTransactionIsolation(connectionProperty.get("defaultTransactionIsolation").toString().toInteger())
        }
        return new DataSource(p)
    }
```

-----

순서
BootStrap.groovy 에서 DB Connection Pool 생성 시 필요한 DB Properties 를 
```groovy
private static final Map<String, Properties> dbPropertiesMap = [:]
```
에 저장? 함.
==static final 키워드는 해당 필드가 클래스의 인스턴스 간에 공유되며, 한번 초기화 되면 그 값이 변경 되지 않음을 의미함....
즉 변수 자체의 참조가 변경되지 않는다는 것이고, 변수가 참조하는 객체의 내부 상태는 변경될 수 있음.==

그 후에 Connection Pool 을 생성하고 있지 않다가 TwelveSky2OriService 같은 곳에서 DynamicConnectionPoolManager 에 있는 getDataSource 호출 시 
```groovy
if (!dataSources.containsKey(dataSourceName) || dataSources.get(dataSourceName) == null) {
            Properties dbProps = dbPropertiesMap.get(dataSourceName)
            if (dbProps != null) {
                try {
                    DataSource dataSource = createDataSource(dbProps)
                    dataSources.put(dataSourceName, dataSource)
                } catch (Exception e) {
                    dataSources.put(dataSourceName, null) // 실패 시 null로 설정
                    throw new RuntimeException("Failed to create DataSource for $dataSourceName: ${e.message}", e)
                }
            } else {
                throw new IllegalStateException("No database properties found for: $dataSourceName")
            }
        }else {
```
이 if 절에서 걸려서 createDataSource 로 Connection Pool 을 생성하게 됨.

createDataSource 는
```groovy
PoolProperties p = new PoolProperties()
        String dataSourceName = dbProps.get("dataSourceName") // 실제 사용되는 db 이름
        String dbType = dbProps.get("dbType") // mysql, oracle, postgresql, mssql
        p.setUrl(dbProps.get("url").toString())
        p.setDriverClassName(dbProps.get("dbDriver").toString())
        p.setUsername(dbProps.get("username").toString())
        p.setPassword(dbProps.get("password").toString())  
        def connectionProperty =[:]
        if(Environment.current.name == 'test'){
            connectionProperty = dbType == 'oracle'? DataSourceConfig.dbPropertiesForTestOracle.call() : DataSourceConfig.dbPropertiesForTest.call()
        }else if (Environment.current.name == 'production') {
            connectionProperty = dbType == 'oracle'? DataSourceConfig.dbPropertiesForLiveOracle.call() : DataSourceConfig.dbPropertiesForLive.call()
        }
        if(!connectionProperty.isEmpty()){
            p.setJmxEnabled((Boolean)connectionProperty.get("jmxEnabled"))
            p.setInitialSize(connectionProperty.get("initialSize").toString().toInteger())
            p.setMaxActive(connectionProperty.get("maxActive").toString().toInteger())
            p.setMinIdle(connectionProperty.get("minIdle").toString().toInteger())
            p.setMaxIdle(connectionProperty.get("maxIdle").toString().toInteger())
            p.setMaxWait(connectionProperty.get("maxWait").toString().toInteger())
            p.setMaxAge(connectionProperty.get("maxAge").toString().toInteger())
           p.setTimeBetweenEvictionRunsMillis(connectionProperty.get("timeBetweenEvictionRunsMillis").toString().toInteger())
            p.setMinEvictableIdleTimeMillis(connectionProperty.get("minEvictableIdleTimeMillis").toString().toInteger())
            p.setValidationQuery(connectionProperty.get("validationQuery").toString())
           p.setValidationQueryTimeout(connectionProperty.get("validationQueryTimeout").toString().toInteger())
            p.setValidationInterval(connectionProperty.get("validationInterval").toString().toInteger())
            p.setTestOnBorrow((Boolean)connectionProperty.get("testOnBorrow"))
            p.setTestWhileIdle((Boolean)connectionProperty.get("testWhileIdle"))
            p.setTestOnReturn((Boolean)connectionProperty.get("testOnReturn"))
            p.setJdbcInterceptors(connectionProperty.get("jdbcInterceptors").toString())
            p.setDefaultTransactionIsolation(connectionProperty.get("defaultTransactionIsolation").toString().toInteger())
        }
        return new DataSource(p)
```
이렇게 처음에 dbPropertiesMap 에 저장된 값을 dataSourceName 으로 가져와서 Connection Pool 을 맺는 과정을 거침.


## 이미 있는 Connection Pool 은?
게임 데이터베이스가 점검날 아름답게 점검 때려버리면 Connection Pool 은 잡고 있는 상태로 네트워크만 끊어져 Connection Pool 이 이상하게 된다.
그렇게 다시 DB 연결이 되서 재시도 하게 되면 이미 닫힌 Connection 에 연결을 넣는다는 error 가 나오게 된다.

그러므로 getDataSource 를 할때 
```groovy
}else {
            // 이미 생성된 DataSource에 대한 유효성 검사
            Properties dbProps = dbPropertiesMap.get(dataSourceName)
            DataSource dataSource = dataSources.get(dataSourceName)
            String dbType = dbProps.get("dbType").toString()
            /*
            Connection 이 있다가 네트워크 문제로 끊겼다가 재연결 될때 Exception 이 나옴.
            create 하다가 터졌을 때 dataSource Map 에서 삭제
            valid 통과 시에는 그냥 넘김
             */
            if (!isConnectionValid(dataSource,dbType)) {
                // 유효하지 않은 경우, DataSource 재생성
                try {
                    dataSource = createDataSource(dbProps)
                    dataSources.put(dataSourceName, dataSource)
                } catch (Exception e) {
                    dataSources.remove(dataSourceName) // 실패 시 DataSource 제거
                    throw new RuntimeException("Failed to recreate DataSource for $dataSourceName: ${e.message}", e)
                }
            }
        }
```
이 부분에서 isConnectionValid 를 호출해서 Connection Pool 이 맛탱이가 안가있는지 확인하게 된다.


isConnectionValid 에서는
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
MySQL 의 경우에는 SELECT 1 , Oracle 에 경우에는 SELECT 1 FROM DUAL 이라는 validation query 를 날려서 Connection 을 확인하게 된다. 좀 더 높은 버전에서는 isValid() 라는 녀석이 있지만
버전이 낮아서 SELECT 1 이라는 기인 열전을 하게 되었다 

SELECT 1 을 했을 때 안되면 다시 createDataSource 를 하게 된다.