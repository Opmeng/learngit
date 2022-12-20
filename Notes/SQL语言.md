## 基础

三范式

第一范式（1NF）：原子性（存储的数据应该具有“不可再分性”）]

第二范式（2NF）：唯一性 (消除非主键部分依赖联合主键中的部分字段)（一定要在第一范式已经满足的情况下）

第三范式（3NF）：独立性，消除传递依赖(非主键值不依赖于另一个非主键值)

主键的值不允许修改，也不允许复用(不能使用已经删除的主键值赋给新数据行的主键)。

SQL 支持以下三种注释:

```sql
# 注释
 -- 注释
/* 注释1
   注释2 */
```

数据库创建与使用:

```sql
create database test
	default character set utf8;
use test;
```

### 创建表

```sql
CREATE TABLE mytable (
  id INT NOT NULL AUTO_INCREMENT,
  col1 INT NOT NULL DEFAULT 1,
  col2 VARCHAR(45) NULL,
  col3 DATE NULL,
  PRIMARY KEY (`id`));
```

###  修改表

添加列

```sql
alter table mytable add col char(20);
```

修改列和属性

```sql
-- ALTER TABLE 表名 CHANGE 原字段名 新字段名 字段类型 约束条件
alter table mytable change col col1 char(32) not null default '123';
```

删除列

```sql
alter table mytable drop column col;
```

删除表

```sql
drop table mytable;
```

###  插入

普通插入

```sql
insert into mytable(col1, col2) values(val1, val2);
```

插入检索出来的数据

```sql
insert into mytable1(col1, col2) select col1, col2 from mytable2;
```

将一个表的内容插入到一个新表

```sql
create table newtable AS select * from mytable;
```

###  更新

```sql
update mytable set col = val where id = 1;
```

###  删除

```sql
delete from mytable where id = 1;
```

**TRUNCATE TABLE** 可以清空表，也就是删除所有行。

```sql
TRUNCATE TABLE mytable;
```

使用更新和删除操作时一定要用 WHERE 子句，不然会把整张表的数据都破坏。可以先用 SELECT 语句进行测试，防止错误删除。

###  查询

####  DISTINCT

相同值只会出现一次。它作用于所有列，也就是说所有列的值都相同才算相同。

```sql
select distinct col1, col2
FROM mytable;
```

####  LIMIT

限制返回的行数。可以有两个参数，第一个参数为起始行，从 0 开始；第二个参数为返回的总行数。

返回前 5 行:

```sql
select * from mytable limit 5;

select * from mytable limit 0, 5;

```

返回第 3 ~ 5 行:

```sql
select * from mytable limit 2, 3;
```

#### 排序

- **ASC** : 升序(默认)
- **DESC** : 降序

可以按多个列进行排序，并且为每个列指定不同的排序方式:

```sql
select * from mytable order by col1 desc, col2 asc;
```

####  通配符

通配符也是用在过滤语句中，但它只能用于文本字段。

- **%** 匹配 >=0 个任意字符；
- **_** 匹配 ==1 个任意字符；
- **[ ]** 可以匹配集合内的字符，例如 [ab] 将匹配字符 a 或者 b。用脱字符 ^ 可以对其进行否定，也就是不匹配集合内的字符。

使用 Like 来进行通配符匹配。

```sql
select * from mytable where col like '[^AB]%'; -- 不以 A 和 B 开头的任意文本
```

不要滥用通配符，通配符位于开头处匹配会非常慢。