# Gradle 学习


# Gradle 入门
## 1. Gradle 的 ZIP 解压后目录
- docs：API、 DSL、指南等文档
- init.d：gradle初始化脚本目录
- lib：相关库
- media：一些icon资源
- samples：示例
- src：源文件
- getting-started.html：入门链接
- LICENSE
- NOTICE

## 2. Gradle Wrapper 
### a. 含义：对Gradle一层包装，便于使用统一Gradle构建
### b. 目录结构：
> |--gradle| |--wrapper|  |--gradle-wrapper.jar|  |--gradle-wrapper.properties|--gradlew|--gradlew.bat
- gradle-wrapper.jar：具体业务逻辑实现的`jar`包
- gradle-wrapper.properties：配置文件，包含篇配置信息如下图：
- gradlew：Linux下可执行脚本
- gradlew.bat：Windows下可执行脚本
### c.常用命令
- 生成： `gradle wrapper` , 由`Wrapper Task` 生成
- 配置参数：
```groovy
gradle wrapper --gradle-version XXX用于指定使用的Gradle版本
gradle wrapper --distribution-url XXX用于指定下载Gradle发行版的url地址
```
- 自定义：`task wrapper(type:Wrapper)`{ //配置信息 }

## 3. Gradle日志
### a.日志级别：
### b.日志输出代码：
使用`print`方法，属于`quiet`级别日志：`println 'XX'X`

使用内置`logger`：

### c.日志输出控制：



例如，输出`QUIET`级别及其之上的日志信息：`gradle -q tasks`

## 4.Gradle命令行

查看所有可执行`tasks：./gradlew tasks`

强制刷新依赖：`./gradlew --refresh-dependencies assemble`

多任务调用：`./gradlew clean jar`

查看帮助：`./gradlew -?或./gradlew -h或./gradlew -help`












