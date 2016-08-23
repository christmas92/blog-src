---
title: Mysql语句
date: 2016-07-27 09:57:04
tags:
- Mysql
---
#### 1.DDL(Data Definition Languages)
```sql
use dbname
show databases
show tables
desc tablename
show create table tablename \G

CREATE DATABASE dbname
DROP DATABASE dbname
CREATE TABLE tablename (col_name_1 col_type_1 constraints,col_name_2 col_type_2 constraints,...col_name_n col_type_n constraints)
DROP TABLE tablename
ALTER TABLE tablename MODIFY [COLUMN] [FIRST|AFTER col_name]
ALTER TABLE tablename ADD [COLUMN] [FIRST|AFTER col_name]
ALTER TABLE tablename DROP col_name
ALTER TABLE tablename CHANGE old_col_name [NEW_COLUMN] [FIRST|AFTER col_name]
```
<!-- more -->
#### 2.DML(Data Manipulation Languages)
> ##### 2.1 插入记录
```sql
#插入一条记录
INSERT INTO tablename (field1,field2,...fieldn) VALUES (value1,value2,...valuen)
#插入多条记录
INSERT INTO tablename (field1,field2,...fieldn)
VALUES
(record1_value1,record1_value2,...record1_valuen),
(record2_value1,record2_value2,...record2_valuen),
...
(recordn_value1,recordn_value2,...recordn_valuen)
```
##### 2.2 更新记录
```sql
#更新一个表中的记录
UPDATE tablename SET field1=value1,field2=value2,...fieldn=valuen [WHERE CONDITION]
#多表更新
UPDATE t1,t2,...tn SET t1.field=expr1,tn.fieldn=exprn [WHERE CONDITION]
```
##### 2.3 删除记录
```sql
#单表删除
DELETE FROM tablename [WHERE CONDITION]
#多表删除
DELETE t1,t2,...tn FROM t1,t2,...tn [WHERE CONDITION]
```
**注：不添加条件语句会将表中所有记录删除**
##### 2.4 查询记录
```sql
SELECT * FROM tablename [WHERE CONDITION]
#去重
SELECT DISTINCT field FROM tablename [WHERE CONDITION]
#升序降序
SELECT * FROM tablename [WHERE CONDITON] [ORDER BY field1 [DESC|ASC],field2 [DESC|ASC],...fieldn [DESC|ASC]]
#排序和限制
SELECT ...[LIMIT offset_start,row_count]
#聚合
SELECT [field1,field2,...fieldn] fun_name
FROM tablename
[WHERE CONDITION]
[GROUP BY field1,field2,...fieldn [WITH ROLLUP]]
[HAVING CONDITION]
#内连接
SELECT field1,field2,...fieldn FROM t1,t2 WHERE t1.fieldn = t2.fieldn
#外链接-左连接
SELECT field1,field2,...fieldn FROM t1 LEFT JOIN t2 on t1.fieldn = t2.fieldn
#外链接-右连接
SELECT field1,field2,...fieldn FROM t1 RIGHT JOIN t2 on t1.fieldn = t2.fieldn
SELECT col_name(s) FROM table_name WHERE col_name IN (value1,value2,...)
```

#### 3.DCL(Data Control Languages)
