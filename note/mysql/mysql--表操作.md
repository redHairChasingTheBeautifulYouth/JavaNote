### 创建表

```
create table tablename(cloumn_name_1 column_type constraints,cloumn_name_2 column_type constraints)
```
- cloumn_name 为列名
- cloumn_type 为数据类型
- constraints 为约束条件
---
### 删除表

```
drop table tablename
```

---
### 修改表
- 修改表字段类型

```
alter table tablename modify cloumn_name cloumn_type constraints
```
- 增加表字段

```
alter table tablename add cloumn_name cloumn_type constraints
```
- 修改表字段名称

```
alter table tablename change old_cloumn_name new_cloumn_name new_cloumn_type
```
- 删除表字段

```
alter table tablename drop cloumn_name
```







