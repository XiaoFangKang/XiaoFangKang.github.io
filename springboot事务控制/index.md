# SpringBoot 之手动控制事务

# Spring 的 7 中事务传播方式
事务|解释
:---|:---
`Propagation.REQUIRED`|`代表当前方法支持当前的事务，且与调用者处于同一事务上下文中，回滚统一回滚`（如果当前方法是被其他方法调用的时候，且调用者本身即有事务），如果没有事务，则自己新建事务，
`Propagation.SUPPORTS`|`代表当前方法支持当前的事务，且与调用者处于同一事务上下文中，回滚统一回滚`（如果当前方法是被其他方法调用的时候，且调用者本身即有事务），如果没有事务，则该方法在非事务的上下文中执行
`Propagation.MANDATORY`|`代表当前方法支持当前的事务，且与调用者处于同一事务上下文中，回滚统一回滚`（如果当前方法是被其他方法调用的时候，且调用者本身即有事务）,如果没有事务，则抛出异常
`Propagation.REQUIRES_NEW`|创建一个新的事务上下文，如果当前方法的调用者已经有了事务，则挂起调用者的事务，这两个事务不处于同一上下文，`如果各自发生异常，各自回滚`
`Propagation.NOT_SUPPORTED`|该方法以非事务的状态执行，如果调用该方法的调用者有事务则先挂起调用者的事务
`Propagation.NEVER`|该方法以非事务的状态执行，如果调用者存在事务，则抛出异常
`Propagation.NESTED`|如果当前上下文中存在事务，则以嵌套事务执行该方法，也就说，`这部分方法是外部方法的一部分，调用者回滚，则该方法回滚，但如果该方法自己发生异常，则自己回滚，不会影响外部事务，如果不存在事务，则与PROPAGATION_REQUIRED一样`
`

# 数据库四大特性和MySql事务的隔离级别
## 四大特征
1. 原则性（`Atomicity`）
   

原子性是指事务包含的所有操作要么全部成功，要么全部失败回滚。

2. 一致性（`Consistency`）

一致性是指事务必须使数据库从一个一致性状态变换到另一个一致性状态，也就是说一个事务执行之前和执行之后都必须处于一致性状态。

3. 隔离性（`Isolation`）

隔离性是当多个用户并发访问数据库时，比如操作同一张表时，数据库为每一个用户开启的事务，不能被其他事务的操作所干扰，多个并发事务之间要相互隔离。

4. 持久性（`Durability`）

持久性是指一个事务一旦被提交了，那么对数据库中的数据的改变就是永久性的，即便是在数据库系统遇到故障的情况下也不会丢失提交事务的操作。

## 隔离机制
事务隔离级别|脏读|不可重复读|幻读
---|---|---|---
读未提交|是|是|是
不可重复读|否|是|是
可重复读|否|否|是
串行化|否|否|否

脏读是指在一个事务处理过程里读取了另一个未提交的事务中的数据。（读取未提交的数据）

b、不可重复读是指在对于数据库中的某个数据，一个事务范围内多次查询却返回了不同的数据值，这是由于在查询间隔，被另一个事务修改并提交了。（边读边写）

c、幻读指两个事务同时发生，两个事务修改数据，读到的数据不是自己开始修改的数据。幻读和不可重复读都是读取了另一条已经提交的事务（这点就脏读不同），所不同的是不可重复读查询的都是同一个数据项，而幻读针对的是一批数据整体。（同时写，同时读）

## 数据库事务级别，默认使用Repeatable read级别，列表级别从下往上级别越低。查看级别

`select @@tx_isolation;`

## 如果在没有办法使用注解的时候（比如多线程等），就要使用手动的方式来做事务管理了，这也就是编程式的事务管理。

1）首先加入注解，这就是spring的jdbc框架中提供的事务管理方式
```
    @Autowired
    private PlatformTransactionManager platformTransactionManager;

    @Autowired
    private TransactionDefinition transactionDefinition;
```
2）看一下源码（DataSourceTransactionManagerAutoConfiguration.class、TransactionTemplate.class）

```
@Bean
@ConditionalOnMissingBean({PlatformTransactionManager.class})
public DataSourceTransactionManager transactionManager(DataSourceProperties properties) {
DataSourceTransactionManager transactionManager = new DataSourceTransactionManager(this.dataSource);
if (this.transactionManagerCustomizers != null) {
this.transactionManagerCustomizers.customize(transactionManager);
}

            return transactionManager;
        }

```
![img_2.png](/images/img_2.png)
备注：有兴趣可以了解一下DataSourceTransactionManager的写法和原理。

```
        @Bean
        @ConditionalOnMissingBean
        public TransactionTemplate transactionTemplate() {
            return new TransactionTemplate(this.transactionManager);
        }
```
![img_1.png](/images/img_1.png)

注意，这里的所有事务传播方式包括处理，都需要自己手动去处理。

3）编写方式
```
TransactionStatus transactionStatus = platformTransactionManager.getTransaction(transactionDefinition);
platformTransactionManager.commit(transactionStatus);
platformTransactionManager.rollback(transactionStatus);
```
说明：这里开发事务过后，返回一个事务状态，这个状态记录了东西，用来控制事务的管理，当然，多个事务之间的控制需要人为控制。

![img.png](/images/img.png)

4）编程式的事务控制经量少用，因为控制程度上面来说spring的方式还是来的更加不错，编程式的方式，更多用于在需要事务的时候，没有办法加入事务，才采取手动控制事务的方式。



