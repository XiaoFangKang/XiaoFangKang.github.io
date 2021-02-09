# 批量insert和批量update

# 批量`insert`
## `insert into`和 `insert all into` 和  `insert into select` 区别

1. `insert into ` 是 `mysql` 中使用的批量导入方法
```sql
INSERT INTO t1(field1,field2) VALUES (v101,v102),(v201,v202),(v301,v302),(v401,v402);
```
2. `insert all into`   是`oracle` 中经常使用的方法
```sql
insert all 
   into t1(field1,field2) VALUES  (v101,v102) 
   into t1(field1,field2) VALUES  (v201,v202)
   into t1(field1,field2) VALUES  (v301,v302)
SELECT 1 FROM DUAL   
```
3. `insert into select ` 是常用的批量导入方法
```sql
-- 当没有指定的表时候使用这种方式，将值直接使用 union 连接批量导入
INSERT INTO table2(field1,field2)
    SELECT field1,field2 FROM dual
    union
    SELECT field1,field2 FROM dual
    union
    SELECT field1,field2 FROM dual
```
## `insert into`和 `insert all into` 和  `insert into select` 效率

# `insert into select` 效率最高。 

# 批量 `update`
## 基础方法
 ```sql
UPDATE student s SET s.name = '张三' WHERE   id = 1; 
 ```

## 变相
 ```sql
-- DML，0.015s
 UPDATE student s
 SET s.name = (
   SELECT b.name FROM boy b WHERE s.id = b.id AND s.name != b.name
 )
WHERE EXISTS (
   SELECT 1 FROM boy b WHERE s.id = b.id AND s.name != b.name
 );
 ```
## 快速游标法
```sql
-- DML，0.014s
BEGIN
  FOR cur IN (
    SELECT s.id sid, b.name bname
  FROM student s, boy b
  WHERE s.id = b.id AND s.name != b.name AND s.sex = 'boy'
  ) loop

  UPDATE student s SET s.name = cur.bname WHERE s.id = cur.sid;

  END loop ;
END ;
```


