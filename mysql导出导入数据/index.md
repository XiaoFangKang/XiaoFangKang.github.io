# MySQL 导(入,出)数据


# 导出数据
## 使用 SELECT ... INTO OUTFILE 语句导出数据

1. 以下实例中我们将数据表 runoob_tbl 数据导出到 /tmp/runoob.txt 文件中:
```shell
 SELECT * FROM runoob_tbl 
  INTO OUTFILE '/tmp/runoob.txt';
```
2. 你可以通过命令选项来设置数据输出的指定格式，以下实例为导出 CSV 格式：
```shell
 SELECT * FROM passwd INTO OUTFILE '/tmp/runoob.txt'
     FIELDS TERMINATED BY ',' ENCLOSED BY '"'
     LINES TERMINATED BY '\r\n';
```
3. 在下面的例子中，生成一个文件，各值用逗号隔开。这种格式可以被许多程序使用。
```shell
    SELECT a,b,a+b INTO OUTFILE '/tmp/result.text'
    FIELDS TERMINATED BY ',' OPTIONALLY ENCLOSED BY '"'
    LINES TERMINATED BY '\n'
    FROM test_table;
```
### SELECT ... INTO OUTFILE 语句有以下属性:

* `LOAD DATA INFILE`是`SELECT ... INTO OUTFILE`的逆操作，`SELECT`句法。
  为了将一个数据库的数据写入一个文件，使用`SELECT ... INTO OUTFILE`，
  为了将文件读回数据库，使用`LOAD DATA INFILE`。
* `SELECT...INTO OUTFILE 'file_name'`形式的`SELECT`
  可以把被选择的行写入一个文件中。该文件被创建到服务器主机上，
  因此您必须拥有`FILE`权限，才能使用此语法。
* 输出不能是一个已存在的文件。防止文件数据被篡改。
* 你需要有一个登陆服务器的账号来检索文件。否则 `SELECT ... INTO OUTFILE`
  不会起任何作用。
* 在`UNIX`中，该文件被创建后是可读的，权限由`MySQL`服务器所拥有。
  这意味着，虽然你就可以读取该文件，但可能无法将其删除。

## 导出库表(`mysqldump`)

1. `mysqldump` -u用户名 -p密码 -h主机 数据库 a -w “sql条件” –`lock-all-tables` > 路径
`mysqldump -hhostname -uusername -p dbname tbname>xxxx.sql`
   
2. ** 按指定条件导出数据库表内容。(-w选项 –where)
`mysqldump -hhostname -uusername-p dbname tbname -w'id >= 1 and id<= 10000'--skip-lock-tables > xxxx.sql`

3. 或这下一行
`mysqldump -hhostname -uusername -p dbname tbname --where='unit_id >= 1 and unit_id <= 10000'> ~/xxxx.sql`

### `mysqldump`导出库表详细举例

1. 导出整个数据库

`mysqldump -u 用户名 -p数据库名 > 导出的文件名`

>mysqldump -u breezelark-p mydb > mydb.sql

2. 导出一个表(包括数据结构及数据)

`mysqldump -u 用户名 -p数据库名 表名> 导出的文件名`

>mysqldump -u lingxi -p mydb mytb> mytb.sql

3. 导出一个数据库结构(无数据只有结构)

`mysqldump -u lingxi -p -d --add-drop-table mydb >mydb.sql`

>-d 没有数据–add-drop-table 在每个create语句之前增加一个drop table


# 导入数据
1. mysql -h主机地址 -u用户名 -p用户密码，文件形式。(shell命令行)

`mysql -u root -p dbname < filename.sql`

2. 直接放在命令行(shell命令行)执行一个sql

`mysql -hhostname -uusername -p dbname -e 'select * from tbname limit 1'`

执行后命令行会提示输入数据库密码。

3. 把SQL作为一个输入给MYSQL(shell命令行)

`echo 'select id from dbname.tbname where id = 1;' | mysql -hhostname -ureadonly -preadonly dbname > xxxx.sql`

4. 进入mysql数据库(数据库中执行SQL文件)

`source xxx.sql`







