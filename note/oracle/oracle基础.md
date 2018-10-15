# Oracle

## 概述
Oracle是Oracle公司的数据库，目前使用较多。具有安全，高并发等特性。常用的数据库还有MySQL，DB2，SQL Server等。 

它是关系型数据库（是二维的数据表格，体现现实中实体之间的关系）  

## 实体之间的关系：  

- 一对一（1 v 1）
- 一对多（1 v N）
- 多对多（N v N）

在Java中体现关系：  

1、实现。2、继承。 3、依赖。4、关联。5、聚合。6、组合

## Oracle数据类型

类型 | 说明 | 示例
---|---|---
number | 整型和浮点型 | number(7,2)
varchar2 | 不定长字符串 | varchar2(200)
char | 定长字符串 | char(20)
date | 日期 | sysdate
timestamp | 时间 |
blob | 大二进制对象 | 
clob | 大二进制文本 |


## 数据库表设计
1. 三范式：建表的理论支持
    1. 第一范式  
    表里面必须含有主键（非空且唯一）主键类型number或char 主要是提高效率（索引） 一张表中只能有一个主键，但是主键可以作用在多个字段上（联合主键）
    2. 第二范式  
    针对多对多的，当出现部分依赖的时候，会出现数据冗余。解决方案：将表拆分为两张实体表和一张关系表。
    3. 第三范式  
    针对一对多，传递依赖产生数据冗余。解决方案：采用主外键，进行拆分表。外键（一个表的字段是另一张表的主键或唯一建）

2. 建表语法
    ```sql
    /*
    create table 表名(
        列名 类型(长度) [default 默认值],
        ...
    );
    约束:主键 唯一 非空 外键 自定义 （主键和唯一建Oracle默认创建索引）
    
    创建约束：
        1、在建表时创建
            1）、在列后
            2）、定义完所有的类
        2、在建表后
    
    
    not null只能定义在列后
    
    create table test_student(
        stu_id number(10) [constraint 约束名 primary key],
        stu_name varchar2(20) not null unique,
        email varchar2(20),
        age number(3),
        sex number(1),
        cid number(10),
        constraint 约束名 check(age>0 and age<120),
        constraint stu_fk foreign key(cid) referencs test_classinfo(cid)
    );
    
    在表后添加约束
    
    alter table test_student add constraint stu_ck_sex check(sex=1 or sex=0);
    
    
    添加外键
    
    create table test_classinfo(
        cid number(10) primary key,
        cname varchar2(20),
    );
    
    数据完整性
    在存在外键关联的时候  在删除主记录的时候不允许操作。
    
    */
    
    ```
    
3. 数据操作：

    CRUD：  C（create|insert） R（read|select）U（update） D（delete）
    
    1. 添加  
        ```sql
        
        insert into 表名 (列1,列2...) values (值1,值2...);
        
        insert into 表名 values (值1,值2...);
        
        insert into 表名 select 语句;
        
        
        -- 拷贝表结构
        create table emp_bak as select * from emp e where 1=2
        
        -- 拷贝表结构和数据
        create table emp_bak as select * from emp e where 1=1
        
        -- 拷贝数据
        
        insert into emp_bak select * from emp;
        
        
        
        ```
    2. 修改
        ```sql
        update 表名 set 列名=值,... where ...
        ```
    
    3. 删除
        ```sql
        -- 删除数据
        delete [from] 表名 where 条件
        
        -- 清空表  第一种效率更高
        truncate table 表名
        
        delete [from] 表名 where 1=1
        
        -- 去除表中的重复数据
        delete from emp_bak e where rowid <> (select max(rowid) from emp_bak c where c.empno=e.empno)
        
        -- 删除表的时候删除约束
        drop table emp_bak cascade constraints;
        ```
    4. 查询
        ```sql
        
        -- select from where group by having order by
        
        执行顺序
        
        先from在where（从后往前） 再group by having 再select 最后 order by
        
        
        
        ```
        
## 分页  

```sql

-- 分页  第一种
select b.* from (sleect a.*,rownum rn from (select * from emp e order by e.sal) a where rownum<=10) b where b.rn >=4

-- 第二种
select t.* from dept t,(select rd from (select rd,rn from(select rowid as rd,rownum as rn from dept order by deptno) where rn<20) where rn >2) t1 where t.rowid=t1.rd;

```





