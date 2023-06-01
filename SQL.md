# SQL 学习
---
> - 由于SQL 的代码记录没办法像 python 文件或者 C 那样被记录，所以我就单独写一个markdown来记录
> - 同时笔记部分利用了 github + iPIC 实现了Github 为基础的图床

# 第一章

---

<br>

## 1-1. 数据库是什么

> - 关系数据库：采用行和列组成的二维表来管理数据
>
> <img src="https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230529144019706.png" alt="image-20230529144019706" style="zoom:50%;" align="left" />
>
> - 管理这类数据表的管理系统就是 **关系库数据管理系统（RDBMS）**

## 1-2. 数据库结构

> - 最常见的结构就是：客户端/服务器类型（C/S）类型

![image-20230529144419544](https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230529144419544.png)

### 表的结构
---
- 数据库和表的关系:

![image-20230529144831887](https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230529144831887.png)

- 表的示例：

<img src="https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230529145228831.png" alt="image-20230529145228831" style="zoom:41%;" align="left" />

- 字段：表的列
- 记录：表的行（**关系数据表必须以行为单位进行读取**）
- 单元格：行列交汇的一个方格（**一个单元格一个数据**）

<br>

## 1-3. SQL 概要

---

> - SQL 用关键字、表名、列名等组合而成的一条语句(SQL 语句)来描述操作的内容

### SQL的分类：

![image-20230529150029342](https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230529150029342.png)

![image-20230529150039864](https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230529150039864.png)

![image-20230529150050689](https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230529150050689.png)

- 用的最多的是：DML

```sql
# 一个非常重要的 DCL 

START TRANSACTION;	-- 开始一个事务。当你执行该命令后，后续的数据库操作语句将被视为一个整体，直到执行 COMMIT; 命令或者回滚事务

......
......

COMMIT;	-- 用于提交事务，将事务中的所有操作永久保存到数据库中
```



### 数据的书写:

<img src="https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230529151010713.png" alt="image-20230529151010713" style="zoom:50%;" align="left" />

<br>

## ==1-4. 表的创建==

---

### 1. 数据库的创建

~~~sql
CREATE DATABASE <数据库名称>;
~~~

### 2. 表的创建

~~~sql
CREATE TABLE <表名> (
	<列名1><数据类型><该列的约束>,
	<列名2><数据类型><该列的约束>,
	<列名3><数据类型><该列的约束>,
	......
	<表的约束1><表的约束2>,......);
~~~

eg.

```sql
CREATE TABLE Addressbook (
    register_no INTEGER NOT NULL,
    name VARCHAR(128) NOT NULL,
    address VARCHAR(256) NOT NULL,
    tel_no CHAR(10),
    PRIMARY KEY (register_no)
)
```



### ==3. 数据类型的指定==

---
| 声明数据的关键字 | 作用 |
| :----------------: | ---- |
| integer          | 用来指定存储整数的列的数据类型(数字型)，不能存储小数。 |
| char | 可以像 CHAR(10) 或者 CHAR(200) 这样，在括号中指定该列可以存储的字符串的长度(最大长度) |
| varchar | VARCHAR 型也是用来指定存储字符串的列的数据类型(字符串类型) |
| date | 用来指定存储日期(年月日)的列的数据类型(日期型) |

- CHAR：字符串以**定长字符串**的形式存储在被指定为 CHAR 型的列中。
  - 所谓定长字符串，就是当列中存储的字符串长度达不到最大长度的时候，使用半角空格进行补足
  - <img src="https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230529154350387.png" alt="image-20230529154350387" style="zoom:50%;" />
- VARCHAR：该类额列是可以用**可变长字符串**来确定的
  - 可变长字符串与定长字符串不同，即使字符数未达到最大长度，也不会用半角空格补足

### ==4. 约束的设置==

---

|        约束关键字        | 作用                                             |
| :----------------------: | ------------------------------------------------ |
|         NOT NULL         | 该列设置了不能输入空白，也就是必须输入数据的约束 |
| PRIMARY KEY(column name) | 特定一行数据，也可以说是唯一确定一行数据         |

## ==1-5. 表的删除和更新==

---

### 1. 表的删除

~~~sql
DROP TABLE <表名>;
~~~

### ==2. 表定义的更新==

#### 2. 添建表的一列

```sql
ALTER TABLE <表名> ADD COLUMN <列定义>;
```

eg. 

```sql
ALTER TABLE <表名> ADD COLUMN product_name_pinyin VARCHAR(100) NOT NULL;
```

#### 3. 删除表的一列

```sql
ALTER TABLE <表名> DROP COLUMN <列名>;
```

eg.

```sql
ALTER TABLE <表名> DROP COLUMN product_name_pinyin;
```

#### 4. 变更表名

```sql
ALTER TABLE <表名> RENAME TO <表名>;
```

#### 5. 参看表的结构

```sql
DESCRIBE <表名>;
```

![image-20230529171205807](https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230529171205807.png)

#### 6. 修改表的名字

```sql
RENAME TABLE <表名> TO <表名>;
```

#### 7. 完表格中添加一列记录

```sql
# 指定列的插入数据
INSERT INTO PRODUCT (<列名>, ...) VALUES (<对应的数据类型>, ...);

# 全部一一对应插入
INSERT INTO PRODUCT VALUES(<全部对应数据>, ...)
```

#### 8. 修改表中多个列的名字

```sql
ALTER TABLE <列名>
RENAME COLUMN old_column1 TO new_column1,
RENAME COLUMN old_column2 TO new_column2,
...;
```



# 第二章

---

<br>

## 2-1. SELECT语句基础

---

> 通过 SELECT 语句查询并选取出必要数据的过程称为查询匹配或查询(query)

### 1. 选出其中几列

```sql
SELECT <列名>,... FROM <表名>
```

### 2. 选出所有列

> 这么写的话，就不能指定顺序了，怎么返回就是按照表列怎么来

```sql
SELECT * FROM <表名>
```

### ==3. 为列设定别名==

> 使用 AS 为列取别名

```sql
SELECT product_id AS id, 
			 product_name AS name, 
			 purchase_price AS price
FROM PRODUCT;
```

- 原本结构

![image-20230601154719474](https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230601154719474.png)

- 取别名结果

![image-20230601154835007](https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230601154835007.png)

#### 别名中文的时候，记得使用双引号("")

```sql
SELECT project_id AS "商品编号", 
	 		project_name AS "商品名", 
	 		purchase_price AS "进货单价"
FROM PRODUCT;
```

![image-20230601155113377](https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230601155113377.png)

### ==4. 选择的数据非重复显示==

```sql
SELECT DISTINCT <列名> FROM <表名>;
```

<div style="display:inline-block">
	<img src="https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230601160334635.png" alt="image-20230601160334635" style="zoom:80%;" align="left" />
  <img src="https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230601160407696.png" alt="image-20230601160407696" style="zoom:55%;" align="right" />
</div>

#### 4.1. 对多列使用 DISTINCT

> 两个列数据完全一样才会被省略

```sql
SELECT DISTINCT <列名1>, <列名2> ... FROM <表名>;
```

eg.

```sql
SELECT DISTINCT name, age FROM students;
```

```markdown
id | name    | age															name | age
------------------															---------
1  | John    | 20																John | 20
2  | Jane    | 25								---> 						Jane | 25
3  | John    | 20																Mary | 22
4  | Mary    | 22
```

#### 4.2. 注意不能写成 <列名1>, 无空格<列名2>

```sql
# Wrong
SELECT DISTINCT name,age FROM students;
```

<br>

### ==5. 根据 WHERE 语句来选择记录==

```sql
SELECT <列名>, ....
FROM <表名>
WHERE<条件表达式>;
```

> 如果我们要选出所有的类型是衣服的商品名，我们一般的操作是这样子的

e.g.

```sql
SELECT project_name, project_type FROM PRODUCT WHERE project_type = "衣服";
```

![image-20230601162413380](https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230601162413380.png)

### 6. 写注释的方法

```sql
-- 这个只可以注释一行
SELECT DISTINCT product_id, purchase_price
FROM Product;
```

```sql
/* 这个可以注释
	很多很多行 */
SELECT DISTINCT product_id, purchase_price FROM Product;
```

<br>

## 2-2. 算术运算符和比较运算符

---

<br>

### 1. 算术运算符

```sql
SELECT product_name, sale_price, 
-- 单独一列数据是自己运算法则算出来的
sale_price * 2 AS "sale_price_x2"
FROM Product;
```

![image-20230601163537646](https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230601163537646.png)

#### 1.1 元算法则表

![image-20230601163614600](https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230601163614600.png)

- 也可以使用 ( ) 决定运算优先级

#### 1.2 只使用 SELECT 运算也是可以的

```sql
SELECT (100 + 200) * 3 AS calculation;
```

```markdown
calculation
-----------
				 900
```

### 2. 关于 NULL

- NULL 参加的四则运算返回结果都是 NULL

### 3. 比较运算符

> '不等于' 用 <> 表示

```sql
SELECT product_name, product_type 
FROM Product
-- 价格不等于 500 的商品名和类型
WHERE sale_price <> 500;
```

#### 3.1 比较运算符表

![image-20230601164527260](https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230601164527260.png)

#### 3.2 where 当中甚至还可以嵌入算数运算再比较

> 找出利润 >= 200 的商品信息

```sql
SELECT product_name, sale_price, purchase_price 
FROM Product
WHERE sale_price - purchase_price >= 200;
```

#### 3.3 对字符串数字使用比较运算符也是同理

```sql
-- 创建表
CREATE TABLE Chars (
  chr CHAR(3) NOT NULL, 
  PRIMARY KEY (chr)
);

-- 插入数据
INSERT INTO Chars VALUES ('1'); 
INSERT INTO Chars VALUES ('2'); 
INSERT INTO Chars VALUES ('3'); 
INSERT INTO Chars VALUES ('10'); 
INSERT INTO Chars VALUES ('11'); 
INSERT INTO Chars VALUES ('222');
```

> 选出所有大于2的数据

```sql
SELECT chr 
-- 这里用法特殊点：数据库.表
FROM shop.Chars 
WHERE chr>'2';
```

#### 3.4 不可以对 NULL 使用比较运算符

---

##### 3.4.1 = NULL 条件，尽管数据是 NULL 也不会显示

```sql
# 错误的语句，搜不出来任何结果
SELECT regist_date
FROM Product
WHERE regist_date = NULL;
```

<br>

##### 3.4.2 虽然可以条件筛选数据，但是数据是 NULL 的也不会显示出来

![image-20230601174004553](https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230601174004553.png)

![image-20230601174016514](https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230601174016514.png)

<br>

## 2-3. 逻辑运算符

---

<br>

### 1. NOT 更广义的 <>

```sql
-- 选出所有价格不等于 1200 的商品信息，实现了 <> 操作
-- 但是因为它可以结合比较运算符就可以产生更多的操作
SELECT * FROM Product WHERE NOT sale_price = 1200;
```

### 2. AND 和 OR 运算符

---

> - 在 where 子句中使用 **AND** 和 **OR** 运算符，可以对多个查询对象条件组合

<br>

| 运算符 | 作用                                            |
| :----- | ----------------------------------------------- |
| AND    | AND左右两侧，两个条件都成立的时候才会查询       |
| OR     | AND左右两侧，两个条件只要成立一个的时候就会查询 |

```sql
SELECT product_name, purchase_price FROM Product
WHERE 
product_type = '衣服' AND sale_price >= 400;
```

```sql
SELECT product_name, purchase_price 
FROM Product
WHERE product_type = '衣服' OR product_type = '办公用品';
```

<br>

### 3. 通过括号来强化处理

---

> 问题：“商品种类为办公用品”并且“登记日期是2009年9月11日或者2009年9月20日”应该如何写呢？

```sql
SELECT product_name, product_type, regist_date FROM Product
WHERE 
# Wrong Demo
product_type = '办公用品' AND regist_date = '2009-09-11' OR regist_date = '2009-09-20';

# 误解成
--> (product_type = '办公用品' AND regist_date = '2009-09-11')
OR regist_date = '2009-09-20';
```

- 这个式子得到的结果往往不如人意

- 因为 AND 优先于 OR

- 句子被误解成：“商品种类为办公用品，并且登记日期是 2009 年 9 月 11 日” 或者

  “登记日期是2009年9月20日”

- 这导致什么呢，就相当于两个条件都是一部分，满足一个就行，和我们表达意思就差大了

```sql
# Slove
SELECT product_name, product_type, regist_date FROM Product
WHERE product_type = '办公用品'
AND ( regist_date = '2009-09-11' OR regist_date = '2009-09-20');
```

<br>

### 4. 含有NULL时的真值

---

1. 查询 NULL 时不能使用比较运算符（ = 或者 <> ）， 需要使用 **IS NULL** 运算符或者 **IS NOT NULL** 运算符
2. NULL 是真假之外的第三种值，不确定
3. NULL 的逻辑运算规则

![image-20230601181652102](https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230601181652102.png)

<br>

# 第三章

---

