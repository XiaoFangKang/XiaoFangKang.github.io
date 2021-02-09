# ORA-01033:oracle initialization or shutdown in progress 解决办法


# 解决方法

用PL/SQL连接Oracle数据库，输入登录名和密码后，提示如下错误：
<span style="color:red">ora-01033:oracle initialization or shutdown in progress</span> ；

第一步，运行cmd，输入`sqlplus /nolog`，如图
![](/images/ORA-01033/ORA-01033-1607665707999.png)
第二步、`SQL>connect / as sysdba`

第三步、`SQL>shutdown normal`

第四步、`SQL>startup mount`

第五步、`SQL>alter database open;`
![](/images/ORA-01033/ORA-01033-1607665830272.png)

## 提示:

第1 行出现错误:<span style="color:red">ORA-01157</span> :
无法标识/锁定数据文件12 - 请参阅 `DBWR` 跟踪文件 <span style="color:red">ORA-01110</span>
: 数据文件12: ''。。。''

**ps: 这个提示文件部分（12）根据每个人不同情况有点差别。**

第六步、`SQL>alter database datafile 12 offline drop`;

第七步、重复使用第五第六步（一直循环这个语句，直至不再提示错误），直到出现“数据库已更改”的提示，然 后如下图，
![](/images/ORA-01033/ORA-01033-1607666342224.png)

第八步、继续执行`shutdown normal`，`startup`就OK啦

已经解决完成，现在可以关闭重新登录下`PLSQL`了。
