# 查看oracle数据库的连接数以及用户【转】


1. 查询 `oracle`的连接数

`select count(*) from v$session;`

2. 查询`oracle`的并发连接数

`select count(*) from v$session where status='ACTIVE';`
   
3. 查看不同用户的连接数

`select username,count(username) from v$session where username is not null group by username;`

4. 查看所有用户：

`select * from all_users;`

5. 查看用户或角色系统权限(直接赋值给用户或角色的系统权限)：

`select * from dba_sys_privs;`

`select * from user_sys_privs;`

6. 查看角色(只能查看登陆用户拥有的角色)所包含的权限

`select * from role_sys_privs;`

7. 查看用户对象权限：

`select * from dba_tab_privs;`

`select * from all_tab_privs;`

`select * from user_tab_privs;`

8. 查看所有角色：

`select * from dba_roles;`

9. 查看用户或角色所拥有的角色：

`select * from dba_role_privs;`

`select * from user_role_privs;`

10. 查看哪些用户有`sysdba`或`sysoper`系统权限(查询时需要相应权限)

`select * from V$PWFILE_USERS;`
   
`select count(*) from v$process` --当前的连接数

`select value from v$parameter where name = 'processes' `--数据库允许的最大连接数

**修改最大连接数:**

`alter system set processes = 300 scope = spfile;`

**重启数据库:**

`shutdown immediate;`
`startup;`

**--查看当前有哪些用户正在使用数据**

```sql
SELECT osuser, a.username,cpu_time/executions/1000000||'s', sql_fulltext,machine
from v$session a, v$sqlarea b
where a.sql_address =b.address order by cpu_time/executions desc;
```

`select count(*) from v$session` #连接数

`select count(*) from v$session where status='ACTIVE'`　#并发连接数

`show parameter processes` #最大连接

`alter system set processes = value scope = spfile;`重启数据库 #修改连接


```shell
SQL> Select count(*) from v$session where status='ACTIVE' ;

COUNT(*)
----------
20

SQL> Select count(*) from v$session;

COUNT(*)
----------
187

SQL> show parameter processes;

NAME TYPE VALUE
------------------------------------ ----------- ----------
aq_tm_processes integer 0
db_writer_processes integer 1
gcs_server_processes integer 0
job_queue_processes integer 10
log_archive_max_processes integer 2
processes integer 450
SQL>
```
**并发指`active,I SEE`**

```shell
SQL> select count(*) from v$session #连接数
SQL> Select count(*) from v$session where status='ACTIVE'　#并发连接数
SQL> show parameter processes #最大连接
SQL> alter system set processes = value scope = spfile;重启数据库 #修改连接
```
`unix` 1个用户`session` 对应一个操作系统 `process`
而 `windows`体现在线程

`DBA`要定时对数据库的连接情况进行检查，看与数据库建立的会话数目是不是正常，如果建立了过多的连接，会消耗数据库的资源。同时，对一些“挂死”的连接，可能会需要
`DBA`手工进行清理。

以下的`SQL`语句列出当前数据库建立的会话情况:

`select sid,serial#,username,program,machine,status
from v$session;`

**输出结果为:**
```text
SID SERIAL# USERNAME PROGRAM MACHINE STATUS
---- ------- ---------- ----------- --------------- --------
 1 ORACLE.EXE WORK3 ACTIVE
 1 ORACLE.EXE WORK3 ACTIVE
 1 ORACLE.EXE WORK3 ACTIVE
 1 ORACLE.EXE WORK3 ACTIVE
 3 ORACLE.EXE WORK3 ACTIVE
 1 ORACLE.EXE WORK3 ACTIVE
 1 ORACLE.EXE WORK3 ACTIVE
 27 SYS SQLPLUS.EXE WORKGROUP\\WORK3 ACTIVE
 5 DBSNMP dbsnmp.exe WORKGROUP\\WORK3 INACTIVE
```
**其中，**
`SID `会话(`session`)的`ID`号;

`SERIAL`# 会话的序列号，和`SID`一起用来唯一标识一个会话;

`USERNAME` 建立该会话的用户名;

`PROGRAM` 这个会话是用什么工具连接到数据库的;

`STATUS` 当前这个会话的状态，`ACTIVE`表示会话正在执行某些任务，`INACTIVE`
表示当前会话没有执行任何操作;
如果`DBA`要手工断开某个会话，则执行:

`alter system kill session \'SID,SERIAL#\'`

`sql`语句

**`SQL`语句如下：**

```sql
SELECT username, machine, program, status, COUNT (machine) AS
连接数量
FROM v$session
GROUP BY username, machine, program, status
ORDER BY machine;
```

**显示结果（每个人的机器上会不同）**

```text
SCHNEIDER|WORKGROUD\WANGZHENG|TOAD.exe|ACTIVE|1
SCHNEIDER|WORKGROUP\597728AA514F49D|sqlplusw.exe|INACTIVE|1
|WWW-Q6ZMR2OIU9V|ORACLE.EXE|ACTIVE|8
PUBLIC|||INACTIVE|0
```



**按主机名查询**

`SELECT COUNT(*) FROM V$SESSION WHERE MACHINE = 'DXMH';` '`DXMH`'为主机名



**数据恢复语句**

```sql
create table informationlaw_bak
as
select * from informationlaw as of TIMESTAMP to_timestamp('20121126 103435','yyyymmdd hh24miss');
```



**//按机器名分组查**

```sql
 select username,machine,count(username) from v$session where username is not null group by username,machine;
```



本文章转载于:[PeterWang2018](https://blog.51cto.com/wangqh/1787260)



