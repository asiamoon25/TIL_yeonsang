```plantuml
class DataSourceConfig {
    + dbPropertiesForTestOracle() : Closure
    + dbPropertiesForTest() : Closure
    + dbPropertiesForLiveOracle() : Closure
    + dbPropertiesForLive() : Closure
}

class DynamicConnectionPoolManager {
    - dataSources : Map<String, DataSource>
    + addDbProperties(String, Properties) : void
    + getDataSource(String) : DataSource
    + closeAll() : void
}

class DataSourceHelper {
    + {static} getAuditionConnectionInfo() : Properties
    + {static} getGameConnectionInfo(String) : Properties
    + {static} ... : Properties
}

DataSourceConfig --> "returns" Properties : creates
DataSourceHelper --> "returns" Properties : creates
DynamicConnectionPoolManager -right-> DataSource : manages
```


