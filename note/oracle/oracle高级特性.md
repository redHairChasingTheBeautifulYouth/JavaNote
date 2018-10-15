# 高级特性

## 函数库
Oracle有强大的函数库：  
```sql

-- case when
-- nvl(列，默认值)  当指定的列的值为null时返回默认值
-- 相当于 if(列 == null) return 默认值;

-- 比如  现在要计算emp表中的 sal和comm的和
select e.*,(e.sal+e.comm) from emp e;
-- null 和任何值计算都为null
-- 所以需要默认值
select e.*,(e.sal+nvl(e.comm,0)) from emp e;


-- decode 相当于 switch
-- decode(列，值，显示值，值，显示值，显示值)
select e.*,decode(e.job,'PRESIDENT','牛人','MANAGER','小牛人','普通人') from emp e;

```

## 常用函数列表
分类 | 函数
---|---
字符串 | trim、length、replace、concat、lower、upper、ltrim、rtrim
数值 | ceil、floor
日期 | sysdate、add_months、last_daty、trunc、months_between
转换 | to_number、to_char、to_date
组函数 | max、min、avg、count、sum
分析 | sum()、over()、rank()
其他 | decode、nvl、rownum、rowid


## 练习

1、用一个查询语句，实现查询各个岗位的总工资和各个部门的总工资和所有雇员的总工资  
```sql

-- 第一种写法
select '各个岗位总工资',e.job,sum(e.sal) from emp e group by e.job
union all
select '各个部门总工资',to_char(e.deptno) ,sum(e.sal) from emp e group by e.deptno
union all
select '所有雇员总工资','', sum(e.sal) from emp e;

/*
    union 和 union all区别  
    union：如果有两条记录完全一样的时候  会自动合并  
    union all：不管记录怎么样  都不会合并
*/

-- 第二种写法
-- 采用 over函数进行分析

select e.*,sum(e.sal) over() 所有雇员总工资 from emp e;

-- 第三种写法

select e.job,e.deptno ,sum(e.sal) from emp e group by grouping sets((e.job),(e.deptno),(null))


```


