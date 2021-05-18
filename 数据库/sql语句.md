# 零、其他

## 1.DDL

Data Definition Language，数据定义语言。

用来创建或删除存储数据用的数据库以及库中的表等对象。

1.create：创建数据库和表等对象。

2.drop：删除数据库和表等对象。

3.alter：修改数据库和表等对象的结构。

## 2.DML

Data Manipulation Language，数据操纵语言。

用来查询或者变更表中的记录。

1.select：查询表中的数据。

2.insert：向表中插入数据。

3.update：更新表中的数据。

4.delete：删除表中的数据。

## 3.DCL

Data Control Language，数据控制语言。

用来确认或者取消对数据的变更。还可以赋予和变更使用者对数据库的操作权限。

1.commit：确认对数据库中的数据进行变更。

2.rollback：取消对数据库中的数据进行变更。

3.grant：赋予用户操作权限。

4.revoke：取消用户操作权限。

## 4.其他注意

1.sql不区分**关键字**的大小写。

2.sql用分号（；）结尾。

3.字符串和日期要用单引号（''）括起来。

4.数字常熟无需单引号。



# 一、创建数据库和表

## 1.数据库字段类型

1.integer：整数。

2.char：固定长度的字符串。

3.varchar：可变长度的字符串。

4.date：用来存储日期，包含年月日。oracle中date类型还包含时分秒。

## 2.设置约束

1.NOT NULL：表示该记录不能为空。

2.PRIMARY KEY：设置主键。主键不能为空，同表唯一且不能重复。

## 3.创建数据库

```sql
create database <数据库名称>;
```

## 4.创建数据库的表

```sql
create table <表名>
(
    <列名1> <数据类型> <该列所需约束>,
    <列名2> <数据类型> <该列所需约束>,
    <列名3> <数据类型> <该列所需约束>,
    --.......
    <列名N> <数据类型> <该列所需约束>,
);
```

## 5.删除表

```sql
drop table <表名>;
```

## 6.改变表中的字段

### 1.添加字段

```sql
alter table <表名> add column <列的定义>;--mysql/db2/PostgreSQL
alter table <表名> add <列名>;--oracle/sql server
alter table <表名> add (<列名1>,<列名2>,<列名N>);--oracle添加多列
```

### 2.删除字段

```sql
alter table <表名> drop column <列名>;--mysql/....
alter table <表名> drop <列名>;--oracle
alter table <表名> drop (<列名1>,<列名2>,<列名N>);--oracle删除多列
```

### 3.修改字段

```sql
alter table <变更前字段名> rename to <变更后字段名>;--oralce/PostgreSQL
rename table <变更前字段名> to <变更后字段名>;--db2
sp_rename '<变更前字段名>','<变更后字段名>';--sql server
rename table <变更前字段名> to <变更后字段名>;--mysql
```

## 7.向表中插入数据

```sql
begin transaction;--oracle/db2
start transaction;--mysql
insert into <表名> values (<列1的值>,<列2的值>,<列N的值>);
commit;--确定插入
```

## N.例子：

```sql
--创建数据库
create database shop;

--创建数据库表
create table Product
(
    product_id		char(4)			NOT NULL,
    product_name	varchar(100)	NOT NULL,
    product_type	varchar(32)		NOT NULL,
    sale_price		integer					,
    purchase_price	integer					,
    regist_date		date					,
    PRIMARY KEY		(product_id)
);

--删除Product表
drop table Product;

--向表中添加字段
alter table Product add column product_name_pinyin VARCHAR(100);--mysql
alter table Product add (product_name_pinyin VARCHAR(100));--oracle
	
--删除表中字段
alter table Product drop column product_name_pinyin;--mysql
alter table Product drop (product_name_pinyin);--oracle

--修改表中字段
alter table Poduct rename to Product;--oracle/PostgreSQL
rename table Poduct to Product;--db2
sp_rename 'Poduct','Product';--sql server
rename table Poduct to Product;--mysql
```



# 二、查询语句

## 1.基本查询

```sql
select <列名1>,<列名2>,<列名N>
from <表名>;
```

1.查询结果中列的顺序和select子句中的顺序相同。

2.想要查询出全部列时，可以用星号（*）代替所有列。但是显示顺序会和创建时候的一样。

## 2.为列设定别名

```sql
select <列名1> as <别名1>,
		<列名2> as <别名2>,
		<列名N> as <别名N>,
from <表名>;
```

1.别名在使用中文时需要用双引号（""）括起来。

## 3.查询使用常数

```sql
select <自定义常数> as <自定义别名>,
		<列名1> as <别名1>,
		<列名2> as <别名2>
from <表名>;
```

查询出来的内容，第一列会是自定义别名，并且自定义别名下的值全部为自定义常数。

## 4.从结果中删除重复行distinct

```sql
select distinct <列名>
from <表名>;
```

1.在使用distinct的时候，NULL也被视为一条数据。也就是两条NULL也会被合并为一条。

2.distinct关键字只能用在第一个列名之前。

## 5.根据where语句来选择记录

```sql
select <列名1>,<列名2>,<列名N>
from <表名>
where <条件表达式>;
```

首先通过where子句查询出符合指定条件的记录，然后再选取出select语句指定的列。

1.sql中子句的书写顺序是固定的，不能随意更改。where必须紧跟在from之后。

## N.例子：

```sql
--基本查询
select product_id, product_name, purchase_price
from Product;

--查询表中所有列
select * from Product;

--查询取别名
select 	product_id		as "商品编号",
		product_name	as "商品名称",
		purchase_price	as "进货单价"
from Product;

--常数查询
select	'Product'		as string,
		38				as number,
		'2001-04-24'	as date,
		product_id,
		product_name
from Product;

--从结果中删除重复行
select distinct product_type
from Product;

--使用where进行条件查询
select product_name, product_type
from Product
where product_type = '衣服';



```

