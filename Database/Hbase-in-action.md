#hbase in action
---
#API client
所有修改操作行级原子性
创建HTable实例需要扫描.META表，推荐只创建一次，每个线程创建一个，生存期复用这个对象；需要多个HTable实例，考虑使用HTablePool

##CRUD
HbaseConfiguration
```
static Configuration create();//尝试从classpath家中hbase-default.xml，hbase-site.xml
static Configuration create(Configuration that);
```
##PUT
add
未指定时间戳，将由region服务器设定为服务器当前时间，因此必须确保服务器时间正确
默认情况，hbase保留3个版本数据

###激活缓冲区
```
table.setAutoFlush(false);//默认true不开启
isAutoFlush();//检查
```
开启后，单行put部产生RPC调用，flushCommits()强制写服务端
缓冲区大小配置：
```java
long getWriteBufferSize();
void setWriteBufferSize(long writeBufferSize) throws IOException;//默认2MB
```
hbase-site.xml配置
```xml
<property>
	<name>hbase.client.write.buffer</name>
	<value>20971520</value><!--20MB-->
</property>
```
隐式刷写：
调用put()或setWriteBufferSize时，比较占用缓冲区和配置大小，超出限制，触发flushCommits
通过getWriteBuffer()获取写入缓存内容
PS：
* 缓冲区为内存列表，程序停止，如未发送RPC，则数据会丢失
* 内存占用，预估：hbase.client.write.buffer x hbase.regionserver.handler.count x region服务器数量
* 如果只存储大单元，则缓冲区左右不大，主要时间在传输


##GET
默认按版本降序存储，scan,get只返回一个版本
```java
List<KeyValue> get(byte[] family,byte[] qualifier)
Map<byte[], List<KeyValue>> getFamilyMap()

//check
has(byte[] family,byte[] qualifier)
has(byte[] family,byte[] qualifier,long ts)
has(byte[] family,byte[] qualifier, byte[] value)
has(byte[] family,byte[] qualifier,long ts, byte[] value)

//others
getRow //rowkey
getRowLock
getLockId
setWriteToWAL
getWriteToWAL
getTimeStamp
heapSize
isEmpty
numFamilies
size
```




##导数据
[ Bulk Load－HBase数据导入最佳实践](http://blog.csdn.net/opensure/article/details/47054861)

---
#开发
[开发环境搭建](http://blog.csdn.net/chicm/article/details/41787797)

---
#shell
[hbase shell基础和常用命令详解](http://www.jb51.net/article/31172.htm)
##管理查看类
```
hbase shell
status
version
list
```

### DDL
### table
#### create table
create 'tablename','column1','column2','column3'...
create 'gpsInfo', 'baseInfo'
create 'gpsInfoTest', 'baseInfo'

count 'test_gpsinfo'

describe 'tablename'
describe 'gpsInfo'
hbase(main):002:0> describe 'gpsInfo'
DESCRIPTION                                                                         ENABLED
 'gpsInfo', {NAME => 'baseInfo', DATA_BLOCK_ENCODING => 'NONE', BLOOMFILTER => 'NON true E', REPLICATION_SCOPE => '0', VERSIONS => '3', COMPRESSION => 'NONE', MIN_VERSIONS  => '0', TTL => '2147483647', KEEP_DELETED_CELLS => 'false', BLOCKSIZE => '65536', IN_MEMORY => 'false', ENCODE_ON_DISK => 'true', BLOCKCACHE => 'true'}


#### del table
disable 'tablename'
drop 'tablename'

#### scan table
scan 'gpsInfo',{LIMIT=>100}
scan 'gpsInfo123',{LIMIT=>5}
scan 'D_AREAQUERY',{LIMIT=>10}

#### other oper
exists 'tablename'
is_enabled 'tablename'
is_disabled 'tablename'


### column

#### del column
* disable table : disable 'tablename'
* alter table:  alter 'tablename',{NAME=>'columnname',METHOD=>'delete'}
* enable 'tablename'

### DML
#### add data
put <table>,<rowkey>,<family:column>,<value>,<timestamp>
put 'gpsInfoTest','0000000320101227','baseInfo:081351','01010200202010000003\x00;2010-12-27 08:13:51\x00;109.10437\x00;36.64465\x00;',1293408831000

put 'user','andieguo','info:age','27'

#### get data
get <table>,<rowkey>,[<family:column>,....]
get 'gpsInfoTest','0000000320101227','baseInfo:081351'

get 'user','andieguo',{COLUMN=>'info:age',TIMESTAMP=>1409304}

get 'gpsInfoTest','0000000320101227','info'

#### del data
delete  '表名' ,'行名称' , '列名称'
delete 'test_gpsinfo','0101024050602010796620150325','baseInfo'

delete 'test_gpsinfo','0101024050602010796620150325','baseInfo:113922'

put '表名称', '行名称', '列名称:', '值'
status
version

##### del row
deleteall 'gpsInfoTest','null20150611'

#### truncate table
truncate 'tablename'

#### hbase分页
http://ronxin999.blog.163.com/blog/static/422179202013621111545534/


