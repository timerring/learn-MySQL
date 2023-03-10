- [Basic chapter 3 - 基本的SELECT语句](#basic-chapter-3---基本的select语句)
  - [1.SQL概述](#1sql概述)
    - [SQL背景知识](#sql背景知识)
    - [SQL 分类](#sql-分类)
  - [2.SQL语言的规则与规范](#2sql语言的规则与规范)
    - [关于标点符号](#关于标点符号)
    - [SQL大小写规范](#sql大小写规范)
    - [注 释](#注-释)
    - [命名规则](#命名规则)
    - [数据导入指令](#数据导入指令)
  - [3. 基本的SELECT语句](#3-基本的select语句)
    - [SELECT...](#select)
    - [SELECT ... FROM](#select--from)
    - [列的别名](#列的别名)
    - [去除重复行](#去除重复行)
    - [空值参与运算](#空值参与运算)
    - [着重号](#着重号)
    - [查询常数(查询同时添加常数字段)](#查询常数查询同时添加常数字段)
  - [4. 显示表结构](#4-显示表结构)
  - [5. 过滤数据](#5-过滤数据)
  - [练习题](#练习题)


# Basic chapter 3 - 基本的SELECT语句

## 1.SQL概述

### SQL背景知识

1974 年，IBM 研究员发布了一篇揭开数据库技术的论文《SEQUEL：一门结构化的英语查询语言》，直到今天这门结构化的查询语言并没有太大的变化。

SQL（Structured Query Language，结构化查询语言）是使用关系模型的数据库应用语言， 与数据直接打交道，由IBM 上世纪70年代开发出来。后由美国国家标准局（ANSI）开始着手制定SQL标准，SQL 有两个重要的标准，分别是 SQL92 和 SQL99，它们分别代表了 92 年和 99 年颁布的 SQL 标准，我们今天使用的 SQL 语言依然遵循这些标准。**不同的数据库生产厂商都支持SQL语句，但都有特有内容。**

自从 SQL 加入了 TIOBE 编程语言排行榜，就一直保持在 Top 10。

### SQL 分类

SQL语言在功能上主要分为如下3大类：

+ **DDL（Data Definition Languages、数据定义语言）**，这些语句定义了不同的数据库、表、视图、索引等数据库对象，还可以用来**创建、删除、修改数据库和数据表的结构**。
  
  主要的语句关键字包括`CREATE` 、`DROP` 、`ALTER` 等。
  
+ **DML（Data Manipulation Language、数据操作语言）**，用于添加、删除、更新和查询数据库记录，并检查数据完整性。
  
  主要的语句关键字包括`INSERT` 、`DELETE` 、`UPDATE` 、`SELECT` 等**增删改查**。SELECT是SQL语言的基础，最为重要。
  
+ **DCL（Data Control Language、数据控制语言）**，用于定义数据库、表、字段、用户的访问权限和安全级别。
  
  主要的语句关键字包括`GRANT` 、`REVOKE` 、`COMMIT` 、`ROLLBACK` 、`SAVEPOINT` 等。

> 因为查询语句使用的非常的频繁，所以很多人把查询语句单拎出来一类：DQL（数据查询语言）。
>
> 还有单独将COMMIT 、ROLLBACK 取出来称为TCL （Transaction Control Language，事务控制语
> 言）。

## 2.SQL语言的规则与规范

SQL 可以写在一行或者多行。为了提高可读性，各子句分行写，必要时使用缩进。

每条命令以 ; 或 \g 或 \G 结束

关键字不能被缩写也不能分行

### 关于标点符号

+ 必须保证所有的()、单引号、双引号是成对结束的
+ 必须使用英文状态下的半角输入方式
+ **字符串型和日期时间类型的数据可以使用单引号（' '）表示**。虽然mysql中不区分，但是**标准的SQL针对单引号中的文字是区分大小写的。**
+ **列的别名，尽量使用双引号（" "）**，而且不建议省略as

### SQL大小写规范

> MySQL 在 Windows 环境下是大小写不敏感的
>
> MySQL 在 Linux 环境下是大小写敏感的
>
> + 数据库名、表名、表的别名、变量名是严格区分大小写的
> + 关键字、函数名、列名(或字段名)、列的别名(字段的别名) 是忽略大小写的。

统一的书写规范：

**数据库名、表名、表别名、字段名、字段别名等都小写**

**SQL 关键字、函数名、绑定变量等都大写**

### 注 释

+ 单行注释：`#注释文字`  (MySQL特有的方式)
+ 单行注释：`-- 注释文字`  (--后面必须包含一个空格。)
+ 多行注释：`/* 注释文字 */`

### 命名规则

+ 数据库、表名**不得超过30个字符**，变量名限制为29个

+ 必须只能包含 **A–Z, a–z, 0–9, _共63个字符**

+ 数据库名、表名、字段名等对象名中间**不要包含空格**

+ 同一个MySQL软件中，数据库**不能同名**；同一个库中，表不能重名；同一个表中，字段不能重名，必须保证你的字段没有和保留字、数据库系统或常用方法冲突**。如果坚持使用，请在SQL语句中使用`（着重号）引起来**。
  
+ **保持字段名和类型的一致性**，在命名字段并为其指定数据类型的时候一定要保证一致性。假如数据类型在一个表里是整数，那在另一个表里可就别变成字符型了
  
+ 举例：

  ```sql
  #以下两句是一样的，不区分大小写
  show databases;
  SHOW DATABASES;
  #创建表格
  #create table student info(...); #表名错误，因为表名有空格
  create table student_info(...);
  #其中order使用``飘号，因为order和系统关键字或系统函数名等预定义标识符重名了
  CREATE TABLE `order`(
  id INT,
  lname VARCHAR(20)
  );
  select id as "编号", `name` as "姓名" from t_stu; #起别名时，as都可以省略
  select id as 编号, `name` as 姓名 from t_stu; #如果字段别名中没有空格，那么可以省略""
  select id as 编 号, `name` as 姓 名 from t_stu; #错误，如果字段别名中有空格，那么不能省略""
  ```

### 数据导入指令

在命令行客户端登录mysql，使用source指令绝对路径导入

```sql
source d:\xxxx.sql
```

## 3. 基本的SELECT语句

### SELECT...

```sql
SELECT 1+1, 2+2;# 直接这样写相当于下面这句
SELECT 1+1, 2+2 FROM DUAL; # 这里DUAL：伪表
```

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230116204506849.png)

### SELECT ... FROM

语法：

```sql
SELECT 标识选择哪些字段(列)
FROM 标识从哪个表中选择
```

> 例如选择全部列：
>
> ```sql
> SELECT *
> FROM departments;
> ```

一般情况下，除非需要使用表中所有的字段数据，最好不要使用通配符‘*’。使用通配符虽然可以节省输入查询语句的时间，但是获取不需要的列数据通常会降低查询和所使用的应用程序的效率。通配符的优势是，当不知道所需要的列的名称时，可以通过它获取它们。

在生产环境下，**不推荐直接使用SELECT * 进行查询**。

> 选择特定的列：
>
> ```sql
> SELECT department_id, location_id
> FROM departments;
> ```

MySQL中的SQL语句是不区分大小写的，因此SELECT和select的作用是相同的，但是习惯将**关键字大写、数据列和表名小写**。

### 列的别名

重命名一个列(alias 别名)，便于计算。注意，重命名之后结果集中的列会显示别名而非原名。

紧跟列名，也可以在**列名和别名之间加入关键字AS，别名使用双引号**，以便在别名中包含空格或特殊的字符并区分大小写。建议别名简短，AS 可以省略。

> 举例
>
> ```sql
> SELECT last_name "Name", salary*12 "Annual Salary"
> FROM employees;
> ```

### 去除重复行

默认情况下，查询会返回全部行，包括重复行。

```sql
SELECT department_id
FROM employees;
```

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230116212544573.png)

在SELECT语句中使用关键字DISTINCT去除重复行

```sql
SELECT DISTINCT department_id
FROM employees;
```

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230116212631205.png)

针对于：

```sql
SELECT DISTINCT department_id,salary
FROM employees;
```

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230116212742311.png)

注意：

+ `DISTINCT` 需要放到所有列名的前面，如果写成`SELECT salary, DISTINCT department_id`
  `FROM employees` 会报错。
+ `DISTINCT` 其实是对后面所有列名的组合进行去重，如果你想要看都有哪些不同的部门（department_id），只需要写DISTINCT department_id 即可，后面不需要再加其他的列名了。

### 空值参与运算

所有运算符或列值遇到null值，运算的结果都为null。当然可以采用`IFNULL`作为其解决方案。

```sql
SELECT employee_id,salary,commission_pct,
12 * salary * (1 + commission_pct) "annual_sal"
FROM employees;
```

在 MySQL 里面， 空值不等于空字符串。一个空字符串的长度是 0，而一个空值的长度是空。而且，**在 MySQL 里面，空值是占用空间的**。

### 着重号

我们需要保证表中的字段、表名等没有和保留字、数据库系统或常用方法冲突。如果真的相同，请在SQL语句中使用一对``（着重号）引起来。

```sql
# 错误
mysql> SELECT * FROM ORDER;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that
corresponds to your MySQL server version for the right syntax to use near 'ORDER' at
line 1

# 正确
mysql> SELECT * FROM `ORDER`;
```

### 查询常数(查询同时添加常数字段)

SELECT 查询还可以对常数进行查询。对的，就是在 SELECT 查询结果中增加一列固定的常数列。这列的取值是我们指定的，而不是从数据表中动态取出的。

比如说，我们想对 employees 数据表中的员工姓名进行查询，同时增加一列字段`corporation` ，这个字段固定值为 “timerring”，可以这样写：

```sql
SELECT 'timering' as corporation, last_name
FROM employees;
```

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230116213626584.png)

## 4. 显示表结构

使用DESCRIBE 或 DESC 命令，表示表结构。

```sql
DESCRIBE employees;
或
DESC employees;
```

```sql
mysql> desc employees;
+----------------+-------------+------+-----+---------+-------+
| Field | Type | Null | Key | Default | Extra |
+----------------+-------------+------+-----+---------+-------+
| employee_id | int(6) | NO | PRI | 0 | |
| first_name | varchar(20) | YES | | NULL | |
| last_name | varchar(25) | NO | | NULL | |
| email | varchar(25) | NO | UNI | NULL | |
| phone_number | varchar(20) | YES | | NULL | |
| hire_date | date | NO | | NULL | |
| job_id | varchar(10) | NO | MUL | NULL | |
| salary | double(8,2) | YES | | NULL | |
| commission_pct | double(2,2) | YES | | NULL | |
| manager_id | int(6) | YES | MUL | NULL | |
| department_id | int(4) | YES | MUL | NULL | |
+----------------+-------------+------+-----+---------+-------+
11 rows in set (0.00 sec)
```

其中，各个字段的含义分别解释如下：

+ Field：表示字段名称。
+ Type：表示字段类型，这里 `barcode`、`goodsname` 是文本型的，`price` 是整数类型的。
+ Null：表示该列是否可以存储NULL值。
+ Key：表示该列是否已编制索引。`PRI`表示该列是表主键的一部分；`UNI`表示该列是UNIQUE索引的一部分；`MUL`表示在列中某个给定值允许出现多次。
+ Default：表示该列是否有默认值，如果有，那么值是多少。
+ Extra：表示可以获取的与给定列有关的附加信息，例如AUTO_INCREMENT等。

## 5. 过滤数据

```sql
SELECT 字段1,字段2
FROM 表名
WHERE 过滤条件
```

+ 使用WHERE 子句，将不满足条件的行过滤掉
+ WHERE子句紧随 FROM子句

> 举例
>
> ```sql
> SELECT employee_id, last_name, job_id, department_id
> FROM employees
> WHERE department_id = 90 ;
> ```
>
> ![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230116214311689.png)

## 练习题

1.查询员工12个月的工资总和，并起别名为ANNUAL SALARY

基本工资

```sql
SELECT employee_id, last_name, salary * 12 "ANNUAL SALARY"
FROM employees;
```

加权工资

```sql
SELECT employee_id, last_name, salary * 12 * ( 1 + IFNULL(commission_pct,0)) "ANNUAL SALARY"
FROM employees;
```

2.查询employees表中去除重复的job_id以后的数据

```sql
SELECT DISTINCT job_id
FROM employees;
```

3.查询工资大于12000的员工姓名和工资

```sql
SELECT first_name, last_name, salary
FROM employees
WHERE salary > 12000;
```

4.查询员工号为176的员工的姓名和部门号

```sql
SELECT first_name, last_name, department_id
FROM employees
WHERE employee_id = 176;
```

5.显示表 departments 的结构，并查询其中的全部数据

```sql
DESC departments;
SELECT * FROM departments;
```





[返回首页](https://github.com/timerring/learn-MySQL)
