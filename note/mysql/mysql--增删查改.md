### 插入记录
- 指定字段名称
```
insert into tablename (field1,field2) values (value1,value2)
```
- 不指定字段名称

顺序得与字段的顺序一致

```
insert into tablename (value1,value2)
```
- 一次性插入多条记录

```
insert into tablename (field1,field2) values (record1,record2),(record1,record2)
```
---
### 更新记录
- 更新一个表中记录

```
update tablename set field1=value1,field2=value2 where condition
```
- 更新多个表中记录

```
update table_1 t1,table_2 t2 set t1.field1=value1,t2.field2=value2 where condition
```
---
### 删除记录
- 删除一个表中记录

```
delete from tablename where condition
```
- 删除多个表中记录

```
delete t1,t2 from table1 t1,table2 t2 where condition
```
---
### 查询
- 查询不重复的记录

```
select distinct name from user 
```
- 条件查询

也可以用>、<、>=、<=、!= ,多个条件还可以用or、and 
```
select distinct name from user where id=1
```
- order by

desc--降序、asc--升序

```
select name from user where id>1 and id<10 order by name desc
```
- limit 

limit start,cloumn_count

```
select name from user where id>1 and id<10 order by name desc limit 0,5
```
- 聚合操作


```
select [field1,field2],fun_name from tablename [where condition] [group by field1,field2] [with rollup] [having condition]
```
说明：
1. fun_name表示要做的聚合操作，如sum(),count(*),max(),min()
2. group by 后表示要进行聚合的字段
3. with rollup是可选语法，表明是否对分类聚合后的结果再汇总
4. having 对分类后的结果再过滤

注意：where聚合前 尽量选用where

实例：
1. emp表中的各个部门总人数

```
select count(1) from emp group by depno
```
2. 统计公司总人数，各个部门人数

```
select depno,count(1) from emp group by depno with rollup
```

结果如下：
```
depno | count(1)
 1    |   2
 2    |   5
NULL  |   7
```
3. 统计人数大于1的部门

```
select depno,count(1) from emp group by depno having count(1)>1
```
4. 统计所有员工的薪水总额、最高和最低薪水

```
select sum(sal),max(sal),min(sal) from emp
```
5. 统计各部门人数和总人数

```
select depno,count(1) from emp group by depno with rollup
```

- 表连接
1. 左连接：包含左边表中的记录甚至是右边表中没有和它匹配的记录

```
select ename,deptname from emp left jion dept on emp.deptno=dept.deptno
```
2. 右连接：包含右边表中的记录甚至是左边表中没有和它匹配的记录

```
select ename,deptname from emp right jion dept on emp.deptno=dept.deptno
```
- 子查询

用于关联子查询的关键字包含in、not in、=、!=、exists、not exists

表连接很多情况下优化子查询

- 记录联合

union与union all的区别在于union all 把结果集直接合并在一起，union是将union all后的结果去重

```
select depno from emp union all select depno from dept
```













