# Oracle中用exp/imp命令参数详解【转】


# Oracle中用exp/imp命令参数详解

## 1.【用 exp 数 据 导 出】：

### 1.1 将数据库`TEST`完全导出,用户名`system` 密码`manager` 导出到`D:\daochu.dmp`中

```shell
exp system/manager@TEST  rows=y  indexes=y compress=n buffer=65536  
feedback=100000full=y  file=d:\daochu.dmp  
log=d:\daochulog.txt   owner=(ECC_BIZ,ECC_CUSTOMER)
```

|关键字|说明|默认|
|:---|:---|---:|
|USERID|用户名/口令|---|
|FULL|导出整个文件 |(N)|
|BUFFER|数据缓冲区的大小|---|
|OWNER|导出指定的所有者用户名列表|---|
|FILE|输出文件|(EXPDAT.DMP)|
|TABLES|导出指定的表名列表|---|
|COMPRESS |是否压缩导出的文件|(Y)|
|RECORDLENGTH |IO 记录的长度|---|
|GRANTS |导出权限|(Y)|
|INCTYPE|增量导出类型|---|
|INDEXES|导出索引|(Y)|
|RECORD |跟踪增量导出|(Y)|
|ROWS|导出数据行|(Y)|
|PARFILE|参数文件名|---|
|CONSTRAINTS |导出限制 |(Y)|
|CONSISTENT|交叉表一致性|---|
|LOG|屏幕输出的日志文件|---|
|STATISTICS|分析对象(ESTIMATE)|---|
|DIRECT|直接路径|---|
|TRIGGERS|导出触发器|(Y)|
|FEEDBACK|显示每 x 行 (0) 的进度|---|
|FILESIZE|各转储文件的最大尺寸|---|
|QUERY|选定导出表子集的子句|---|
|TRANSPORT_TABLESPACE|导出可传输的表空间元数据|---|
|TABLESPACES|导出指定的表空间列表|---|

### 1.2. 将数据库中`system`用户与`sys`用户的表导出

`exp system/manager@TEST file=d:\daochu.dmp owner=(system,sys)`

### 1.3. 将数据库中的表`table1` 、`table2`导出

`exp system/manager@TEST file=d:\daochu.dmp tables=(table1,table2)`

### 1.4. 将数据库中的表table1中的字段filed1以”00″打头的数据导出

`exp system/manager@TEST file=d:\daochu.dmp tables=(table1) query=\” where filed1like &apos;00%&apos;\”`

<b>上面是常用的导出，对于压缩我不太在意，用`winzip`把`dmp`文件可以很好的压缩。不过在上面命令后面 加上 `compress=y` 就可以了</b>

***

## 2.【用 imp 数 据 导 入】：

### 2.1 将`D:\daochu.dmp` 中的数据导入 `TEST`数据库中。

`imp system/manager@TEST   ignore=y  full=y   file=d:\daochu.dmp  log=d:\daoru.txt`

关键字 |    说明 |    默认
:---|:---|---:|
USERID    |用户名/口令
FULL    |导入整个文件      | (N)
BUFFER    |数据缓冲区大小|
FROMUSER    |所有人用户名列表
FILE    |输入文件|      (EXPDAT.DMP)
TOUSER    |用户名列表
SHOW    |只列出文件内容|    (N)
TABLES    |表名列表
IGNORE    |忽略创建错误    |(N)
RECORDLENGTH    |IO记录的长度
GRANTS    |导入权限    |(Y)
INCTYPE    |增量导入类型
INDEXES    |导入索引    | (Y)
COMMIT    |提交数组插入    | (N)
ROWS    |导入数据行     |(Y)
PARFILE    |参数文件名|
LOG    |屏幕输出的日志文件
CONSTRAINTS    |导入限制|     (Y)
DESTROY    |覆盖表空间数据文件|     (N)
INDEXFILE    |将表/索引信息写入指定的文件
SKIP_UNUSABLE_INDEXES    |跳过不可用索引的维护    |  (N)
FEEDBACK    |每 x 行显示进度
TOID_NOVALIDATE    |跳过指定类型 ID 的验证
FILESIZE    |每个转储文件的最大大小
STATISTICS    |始终导入预计算的统计信息
RESUMABLE    |在遇到有关空间的错误时挂起
RESUMABLE_NAME    |用来标识可恢复语句的文本字符串
RESUMABLE_TIMEOUT    |RESUMABLE 的等待时间
COMPILE    |编译过程, 程序包和函数|     (Y)
STREAMS_CONFIGURATION    |导入 Streams 的一般元数据|     (Y)
STREAMS_INSTANITATION    |导入 Streams 的实例化元数据|     (N)
TRANSPORT_TABLESPACE    |导入可传输的表空间元数据
TABLESPACES    |将要传输到数据库的表空间
DATAFILES    |将要传输到数据库的数据文件
TTS_OWNERS    |拥有可传输表空间集中数据的用户

## 3. imp 演示

### 3.1. 获取帮助

`imp help=y`

### 3.2. 导入一个完整数据库

`imp system/manager file=bible_db log=dible_db full=y ignore=y`

### 3.3. 导入一个或一组指定用户所属的全部表、索引和其他对象

`imp system/manager file=seapark log=seapark fromuser=seapark`

`imp system/manager file=seapark log=seapark fromuser=(seapark,amy,amyc,harold)`

### 3.4. 将一个用户所属的数据导入另一个用户

`imp system/manager file=tank log=tank fromuser=seapark touser=seapark_copy`

`imp system/manager file=tank log=tank fromuser=(seapark,amy) touser=(seapark1, amy1)`

### 3.5. 导入一个表

`imp system/manager file=tank log=tank fromuser=seapark TABLES=(a,b)`

### 3.6. 从多个文件导入

`imp system/manager file=(paycheck_1,paycheck_2,paycheck_3,paycheck_4) log=paycheck,filesize=1G full=y`

### 3.7. 使用参数文件

`imp system/manager parfile=bible_tables.par`

`bible_tables.par`参数文件：

`#Import the sample tables used for the Oracle8i Database Administrator's`

`#Bible.`

`fromuser=seapark touser=seapark_copy file=seapark log=seapark_import`

### 3.8. 增量导入(9i中已经取消)

`imp system./manager inctype= RECTORE FULL=Y FILE=A`

本文章转载于:[大卫.宋博客](http://www.cnblogs.com/songdavid/articles/2435439.html)












   
