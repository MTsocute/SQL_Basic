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

#### 添建表的一列

```sql
ALTER TABLE <表名> ADD COLUMN <列定义>;
```

eg. 

```sql
ALTER TABLE <表名> ADD COLUMN product_name_pinyin VARCHAR(100) NOT NULL;
```

#### 删除表的一列

```sql
ALTER TABLE <表名> DROP COLUMN <列名>;
```

eg.

```sql
ALTER TABLE <表名> DROP COLUMN product_name_pinyin;
```

#### 变更表名

```sql
ALTER TABLE <表名> RENAME TO <表名>;
```

#### 参看表的结构

```sql
DESCRIBE <表名>;
```

![image-20230529171205807](https://cdn.jsdelivr.net/gh/MTsocute/Image_Hosting_Platform@main/uPic/image-20230529171205807.png)

#### 修改表的名字

```sql
RENAME TABLE <表名> TO <表名>;
```

