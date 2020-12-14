# java 远程调试


# 远程JVM启用调试模式
```shell
java
-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=2857
-jar *.jar 
```
## 描述
* `-XDebug` 表示虚拟机启用调试功能
* `-Xrunjdwp` 加载`JDWP`
* `transport` 调试程序JVM使用的进程之间通讯方式
* `dt_socket` socket通讯
* `server=y/n` JVM是否需要作为调试服务器执行
* `address` 调试服务器监听的端口号
* `suspend=y/n` 调试客户端建立连接之后启动虚拟机
* JVM启动之后用验证监听的端口号是否生效了 `netstat -anp | grep 1506`

# tomcat 远程调试
## windows 
进入目录下的`bin`目录，编辑打开 **startup.bat** 
在前面添加：
```shell
SET CATALINA_OPTS=-server -Xdebug -Xnoagent -Djava.compiler=NONE -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=8000 
```
## linux
在**catalina.sh**中的首行添加：
```shell
CATALINA_OPTS="-Xdebug  -Xrunjdwp:transport=dt_socket,address=8000,server=y,suspend=n"
```
# idea 本地调试配置
![图片](https://vkceyugu.cdn.bspapp.com/VKCEYUGU-aliyun-aykdinw922ij4a081f/8c478950-38fa-11eb-880a-0db19f4f74bb.png)

