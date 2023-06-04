# SQL 学习
---
> - 由于SQL 的代码记录没办法像 python 文件或者 C 那样被记录，所以我就单独写一个markdown来记录
> - 同时笔记部分利用了 github + iPIC 实现了Github 为基础的图床

# 第一章

---

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

<<<<<<< HEAD
```sql
# 一个非常重要的 DCL 

START TRANSACTION;	-- 开始一个事务。当你执行该命令后，后续的数据库操作语句将被视为一个整体，直到执行 COMMIT; 命令或者回滚事务

......
......

COMMIT;	-- 用于提交事务，将事务中的所有操作永久保存到数据库中
```



### 不同数据类型的不同书写:
=======
### 数据的书写:
>>>>>>> parent of 46017ce (Update SQL.md)

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



### ==3. 数据类型的声明==

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

## ==1-5. SQL命令==

---

### 1. 表的删除

~~~sql
DROP TABLE <表名>;
~~~

<<<<<<< HEAD
### 2. 添建表的一列
=======
### ==2. 表定义的更新==

#### 添建表的一列
>>>>>>> parent of 46017ce (Update SQL.md)

```sql
ALTER TABLE <表名> ADD COLUMN <列定义>;
```

eg. 

```sql
ALTER TABLE <表名> ADD COLUMN product_name_pinyin VARCHAR(100) NOT NULL;
```

<<<<<<< HEAD
### 3. 删除表的一列
=======
#### 删除表的一列
>>>>>>> parent of 46017ce (Update SQL.md)

```sql
ALTER TABLE <表名> DROP COLUMN <列名>;
```

<<<<<<< HEAD
### 4. 变更表名
=======
eg.

```sql
ALTER TABLE <表名> DROP COLUMN product_name_pinyin;
```

#### 变更表名
>>>>>>> parent of 46017ce (Update SQL.md)

```sql
ALTER TABLE <表名> RENAME TO <表名>;
```

<<<<<<< HEAD
### 5. 参看表的结构
=======
#### 参看表的结构
>>>>>>> parent of 46017ce (Update SQL.md)

```sql
DESCRIBE <表名>;
```

![image-20230529171205807](https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230529171205807.png)

<<<<<<< HEAD
### 6. 修改表的名字
=======
#### 修改表的名字
>>>>>>> parent of 46017ce (Update SQL.md)

```sql
RENAME TABLE <表名> TO <表名>;
```

<<<<<<< HEAD
### 7. 完表格中添加一列记录

```sql
# 指定列的插入数据
INSERT INTO PRODUCT (<列名>, ...) VALUES (<对应的数据类型>, ...);

# 全部一一对应插入
INSERT INTO PRODUCT VALUES(<全部对应数据>, ...)
```

### 8. 修改表中多个列的名字

```sql
ALTER TABLE <列名>
RENAME COLUMN old_column1 TO new_column1,
RENAME COLUMN old_column2 TO new_column2,
...;
```

### ==9. 更新一个单元格内的数据==

```sql
-- SET 决定了列，WHERE 决定了具体行，实现定位准确的单元格
UPDATE <表名>
SET <列名> = 新值		
WHERE <条件>;
```

![image-20230603124511497](https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230603124511497.png)

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
<br>


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

<br>

## 3-1. 对表进行聚合查询

---

<br>

### 1. 聚合函数

---

- 聚合函数表

| 函数名 | 实现功能                     |
| ------ | ---------------------------- |
| COUNT  | 计算表中的记录数（行数）     |
| SUM    | 计算表中数值列中数据的合计值 |
| AVG    | 计算表中数值列中数据的平均值 |
| MAX    | 计算表中数值列中数据的最大值 |
| MIN    | 计算表中数值列中数据的最小值 |

所谓**汇聚**，就是把多汗汇总成一行

### 2. 计算表中数据的行数

----

![image-20230602125357999](https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230602125357999.png)

```sql
SELECT COUNT(参数) FROM <表名>;
```

- 执行结果:

```markdown
count
-----
		 5
```

<br>

#### 2.1 计算 NULL 之外的数据的行数

```sql
SELECT COUNT(<含有NULL1的列>) FROM Product;
```

- 对于COUNT函数来说，参数列不同计算的结果也会发生变化
- 把 <列名> 作为参数，COUNT(<列名>) 会得到 NULL 之外的数据数列
- 把 * 作为参数，COUNT(*) 会得到包括 NULL 在内的所有数据数列

<br>

### 3. 计算合计值

---

#### 3.1 单列合计

```sql
# 单列
SELECT SUM(<列名>) FROM Product;
```

```markdown
sum
---
6100
```

#### 3.2 多列合计

```sql
# 多列
SELECT SUM(<列名>), SUM(<列名>) FROM Product;
```

#### 3.3 对于 NULL 的合计

- 如果以列名为参数，那么在计算之前就已经把 NULL 排除在外了。
- 因此，无论有多少个 NULL 都会被无视。
- **这并不代表着说 NULL 等价于 0 **
<div style="display:inline-block">
<img src="https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230602180121513.png" alt="image-20230602180121513" style="zoom:50%;" /><img src="https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230602180129973.png" alt="image-20230602180129973" style="zoom:50%;" />
</div>
<br>

### 4. 计算平均值

---

```sql
# 单列
SELECT AVG(<列名>) FROM Product;
```

```sql
# 多列
SELECT AVG(<列名>), AVG(<列名>) FROM Product;
```

```markdown
		  	avg
------------------
2096.500000000000000			# 结果显示都是浮点数
```

<br>

### 5. 计算最大值和最小值

---

```sql
# 选出最大、最小值
SELECT MAX(<列名>), MIN(<列名>) FROM Product;
```

#### 5.1 MAX和MIN的对于数据的使用范围更加广泛

- 那就是 SUM/ AVG 函数只能对数值类型的列使用，而MAX/MIN 函数原则上可以适用于任何数据类型的列。
- 包括时间、字符串

```sql
# 列都是时间类型
SELECT MAX(regist_date), MIN(regist_date) FROM Product;
```

![image-20230602181919498](https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230602181919498.png)

<br>

### ==6. 使用聚合函数删除重复值（关键字 DISTINCT）==

----

> 假设，我们现在要找出我们一共有多少个类型的商品（product_type），但是 COUNT 函数并不会区分类别，有多少个就记多少，我们如何剔除重复的呢？s

- 解决方法：

#### 6.1 计算去除重复数据后的行数

```sql
SELECT COUNT(DISTINCT <列名>) FROM Product;
```

#### 6.2 错误写法注意

```sql
SELECT DISTINCT COUNT(<列名>) FROM Product;
```

- 注意 DINSTINCT 一定要写在外面，不然的话，数据的操纵顺序就会是不同的了
- 既然先统计完所有的个数，然后在执行 DISTINCT，删除重复
- 但是这个时候，数量都统计好了，那么删除重复也没意义了，相当于没做删除

#### 6.3 所有聚合函数都可以使用 DISTINCT

```sql
SELECT SUM(DISTINCT sale_price) FROM Product;
```

<br>

## 3-2. 对表进行分组

---

### 1. GROUP BY 子句

```sql
SELECT <列名1>, <列名2>, <列名3>, ... 
FROM <表名>
GROUP BY <列名1>, <列名2>, <列名3>, ...;
```

#### 1.1 按商品种类来统计一下数据行数

```sql
SELECT product_type, COUNT(*) 
FROM Product
GROUP BY product_type;
```

<img src="https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230603122354671.png" alt="image-20230603122354671" style="zoom:90%;" align="left" />

<br>

### 2 聚合键中包含NULL的情况

![image-20230603125436114](https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230603125436114.png)

- 不难看出，如何聚合键中包含 NULL 也会作为一个单独的值统计

<br>

### ==3 WHERE 和 GROUP BY 一并使用==
---
> 使用 WHERE 子句进行汇总处理时，会先根据 WHERE 子句指定的条件进行过滤，然后再进行汇总处理

```sql
SELECT <列名1>, <列名2>, <列名3>, ...
FROM <表名>
WHERE <条件>
GROUP BY <列名1>, <列名2>, <列名3>, ...;
```

e.g

```sql
SELECT purchase_price, COUNT(*) 
FROM Product
WHERE product_type = '衣服' 	# 使用 where 筛选以后，我们只保存 '衣服' 类的商品
GROUP BY purchase_price;
```

- 执行顺序：FROM --> WHERE --> GROUP --> SELECT
  

### 4. 与聚合函数和 GROUP BY 子句有关的常见错误

---

<br>

#### 4.1 在 SELECT 子句中书写了多余的列
---
> ​	在使用 COUNT 这样的聚合函数时，SELECT 子句中的元素有严格的限制。实际上，使用聚合函数时，SELECT 子句中只能存在以下三种元素。
>
> - 常数
> - 聚合函数
> - GROUP BY子句中指定的列名（聚合键）

- **把聚合键之外的列名书写在 SELECT 子句之中**

```sql
SELECT product_name, purchase_price, COUNT(*) 
FROM Product
GROUP BY purchase_price;
```

​	列名 product_name 并没有包含在 GROUP BY 子句当中。因此，该列名也不能书写在 SELECT 子句之中。因为，按照两种 GROUP BY 方式的结果有两种映射，问题也就在这里，他们并不是一一对应的。

​	例如，进货单价是 2800 日元的商品有 “运动 T 恤” 和 “菜刀” 两种， 但是 2800 日元这一行应该对应哪个商品名呢？

![image-20230603134659843](https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230603134659843.png)

<br>

#### 4.2 在**GROUP BY**子句中写了列的别名

- **GROUP BY子句中是不能使用别名的**

```sql
SELECT product_type AS pt, COUNT(*) 
FROM Product
GROUP BY pt;	# 使用 pt 这个别名作为分组依据
```

​	在PostgreSQL和 MySQL 执行上述 SQL 语句并不会发生错误，**但是这种语法并不是通用的**，所以还是不要使用

<br>

#### 4.3 在 **WHERE** 子句中使用聚合函数

- **不可以在 where 中使用聚合函数**

```sql
SELECT product_type, COUNT(*) 
FROM Product
WHERE COUNT(*) = 2 		# 错误
GROUP BY product_type;
```

​	我们是要得到分组下的指定条件的结果，但是问题是 WHERE 的执行都是在分组之前的，那么 WHERE 筛选的结果处执行的聚合函数怎么可能和我们预期一样呢

<br>

### 5. GROUP BY 和 DISTINCT 可以实现一个的结果

```sql
# 都会是选出不重复的结果
SELECT DISTINCT product_type FROM Product;

SELECT product_type 
FROM Product
GROUP BY product_type;
```

<br>

## 3-3. 为聚合结果指定条件

---

> 通过指定条件来选取特定组的方法，既在分组之后的筛选方法

### 3.1 HAVING 子句

- WHERE 子句只能指定记录(行)的条件，而不能用来指定组的条件。对集合指定条件就需要使用其他的子句了，此时便可以用 **HAVING** 子语。

```sql
SELECT <列名1>, <列名2>, <列名3>, ...
FROM <表名>
WHERE <条件>
GROUP BY <列名1>, <列名2>, <列名3>, ...;
HAVING <分组结果的筛选条件>
```

- 执行顺序：SELECT --> FROM --> WHERE --> GROUP BY --> HAVING

e.g

```sql
SELECT product_type, COUNT(*) 
FROM Product
GROUP BY product_type 
HAVING COUNT(*) = 2;		# 分组结果中，该类型是 2 个的组
```

```sql
SELECT product_type, AVG(purchase_price) 
FROM Product 
GROUP BY product_type 
HAVING AVG(purchase_price) >= 400;
```

<br>

### ==3.2 相对于 **HAVING** 子句， 更适合写在 **WHERE** 子句中的条件==

> 有些条件既可以写在 where 也可以写在 having，这些条件就是**聚合键所对应的条件**

- HAVING 实现

```sql
SELECT product_type, COUNT(*)
FROM Product 
GROUP BY product_type 
HAVING product_type="衣服";
```

- WHERE 实现

```sql
SELECT product_type, COUNT(*)
FROM Product 
WHERE product_type="衣服";
GROUP BY product_type;
```

虽然实现都是一样的，但是分开理解，理解成这样是最好的，不会混淆，什么做什么：

- WHERE：指定行返回的结果
- HAVING：指定组返回的结果

<br>

## 3-4 对查询结果进行排序

---

- 不使用 ORDERED BU 的时候，每次一出来的结果哦都市随机的，并不是排序好的

### 1. ORDER BY 子句
---
```sql
SELECT <列名1>, <列名2>, ...
FROM <表名> 
GROUP BY <排序基准列1>, <排序基准列2> ...;
```

#### 1.1 由<条件>升序

```sql
SELECT * FROM Product
ORDER BY sale_price;
```

![image-20230604220827704](https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230604220827704.png)

#### 1.2 书写顺序

![image-20230604220908494](https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230604220908494.png)

#### 1.3 由<条件>降序 【DESC】

```sql
SELECT <列名1>, <列名2>, ...
FROM <表名> 
GROUP BY <排序基准列1>, <排序基准列2> ... DESC;
```

- 升降序的关键字分别是 ASC 和 DESC，对应英文 Ascendent 和 Descendent
- 但是默认的就是升序，所以不用写
- 升序：从小到大、降序：从大到小

<br>

### 2.  指定多个排序键

---

> 这个就是是和 Excel 排序同理的，也就是说 **主键** 和 **辅键** 的关系了。即：当某一个主键，出现同值的时候，再去比较其他的键，再根据那个键的值进行排序。

```sql
SELECT product_id, product_name, sale_price, purchase_price 
FROM Product
ORDER BY sale_price, product_id; [主键, 辅键]
```

- 规则是优先使用左侧的键，如果该列存在相同值的话，再接着参考右侧的键
- 辅键的排序的规则，也是按照升序排序

<br>

### ==3. NULL 的排序==

---

- **使用含有 NULL 的列作为排序键时， NULL 会在结果的开头或末尾汇总显示**

![image-20230604231033577](https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230604231033577.png)

<br>

### 4. 在排序键中使用先使用的别名

---

- 回忆一下 **3-2 中 GROUP BY常见的错误部分**
- 就是不可以使用别名作为 GROUP BY 的<筛选条件名>
- 但是 **ORDER BY** 可以

```sql
SELECT product_id AS id, product_name, sale_price AS sp, purchase􏶔 _price
FROM Product ORDER BY sp, id;
```

<br>

### 5. **ORDER BY **子句中可以使用的列

---

#### 5.1 **SELECT**子句中未包含的列也可以在**ORDER BY**子句中使用

```sql
SELECT product_name, sale_price, purchase_price 
FROM Product
ORDER BY product_id;
```

<br>

#### 5.2 也可以使用聚合函数

```sql
SELECT product_type, COUNT(*) 
FROM Product
GROUP BY product_type 
ORDER BY COUNT(*);
```

<br>

### 6. 不要使用列编号

---

> 还可以使用在SELECT子句中出现的列所对应的编号，是指 SELECT 子句中的列按照从左到右的顺序进行排列时所对应的编号(1, 2, 3, ...)

```sql
-- 通过列名指定排序
SELECT product_id, product_name, sale_price, purchase_price
FROM Product
ORDER BY sale_price DESC, product_id;

-- 通过列编号指定排序
SELECT product_id, product_name, sale_price, purchase_price
FROM Product 
ORDER BY 3 DESC, 1;
```

- 不推荐使用：
  - 增加代码阅读障碍
  - 未来会被取消

# 第四章

---

=======
>>>>>>> parent of 46017ce (Update SQL.md)
