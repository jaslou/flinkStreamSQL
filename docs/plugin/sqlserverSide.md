
## 1.格式：
```
 CREATE TABLE tableName(
     colName cloType,
     ...
     PRIMARY KEY(keyInfo),
     PERIOD FOR SYSTEM_TIME
  )WITH(
     type='sqlserver',
     url='jdbcUrl',
     userName='dbUserName',
     password='dbPwd',
     tableName='tableName',
     cache ='LRU',
     cacheSize ='10000',
     cacheTTLMs ='60000',
     parallelism ='1',
     partitionedJoin='false'
  );
```

# 2.支持版本
 mysql-5.6.35
 
## 3.表结构定义
  
 |参数名称|含义|
 |----|---|
 | tableName | sqlserver表名称|
 | colName | 列名称|
 | colType | 列类型 [colType支持的类型](docs/colType.md)|
 | PERIOD FOR SYSTEM_TIME | 关键字表明该定义的表为维表信息|
 | PRIMARY KEY(keyInfo) | 维表主键定义;多个列之间用逗号隔开|
 
## 4.参数

  |参数名称|含义|是否必填|默认值|
  |----|---|---|----|
  | type | 表明维表的类型 sqlserver |是||
  | url | 连接mysql数据库 jdbcUrl |是||
  | userName | sqlserver连接用户名 |是||
  | password | sqlserver连接密码|是||
  | tableName | sqlserver表名称|是||
  | tableName | sqlserver 的表名称|是||
  | cache | 维表缓存策略(NONE/LRU)|否|NONE|
  | partitionedJoin | 是否在維表join之前先根据 設定的key 做一次keyby操作(可以減少维表的数据缓存量)|否|false|
  
  ----------
  > 缓存策略
  * NONE: 不做内存缓存
  * LRU:
    * cacheSize: 缓存的条目数量
    * cacheTTLMs:缓存的过期时间(ms)

## 5.样例
```
create table sideTable(
    channel varchar,
    xccount int,
    PRIMARY KEY(channel),
    PERIOD FOR SYSTEM_TIME
 )WITH(
    type='sqlserver',
    url='jdbc:jtds:sqlserver://172.16.8.104:1433;DatabaseName=mytest',
    userName='dtstack',
    password='abc123',
    tableName='sidetest',
    cache ='LRU',
    cacheSize ='10000',
    cacheTTLMs ='60000',
    parallelism ='1',
    partitionedJoin='false'
 );


```


