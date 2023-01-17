# learn-MySQL
> Further study and note-taking of MySQL, including principle analysis, practical code, interview questions and SQL cheat sheet.

MySQL的深层学习和笔记，包括原理分析、实用代码、面试题和SQL速查表。

## MySQL 数据库基础篇

[Basic chapter 1 - 数据库概述](https://github.com/timerring/learn-MySQL/blob/main/Basic%20chapter%201%20-%20Database%20Overview.md)

[Basic chapter 2 - MySQL环境搭建](https://github.com/timerring/learn-MySQL/blob/main/Basic%20chapter%202%20-%20MySQL%20Environment%20Setup.md)

[Basic chapter 3 - 基本的SELECT语句](https://github.com/timerring/learn-MySQL/blob/main/Basic%20chapter%203%20-%20Basic%20SELECT%20Statement.md)

[Basic chapter 4 - 运算符](https://github.com/timerring/learn-MySQL/blob/main/Basic%20chapter%204%20-%20Operators.md)

## MySQL 数据库高级篇

Coming Soon...



## MySQL 实用代码库

[相关代码库](https://github.com/timerring/learn-MySQL/tree/main/Codelib)



## SQL速查表

### 注释

| 语法           | 作用     |
| -------------- | -------- |
| # 注释文字     | 单行注释 |
| -- 注释文字    | 单行注释 |
| /* 注释文字 */ | 多行注释 |

### SELECT语句

| 语法                                                         | 作用                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| SELECT 1+1, 2+2 FROM DUAL;                                   | 伪表查询                                                     |
| SELECT department_id, location_id<br/>FROM departments;      | 普通字段查询                                                 |
| SELECT last_name "Name", salary*12 "Annual Salary"<br/>FROM employees; | 列的别名。(列和别名之间加`AS`也行)。                         |
| SELECT DISTINCT department_id<br/>FROM employees;            | 关键字DISTINCT去除重复行                                     |
| SELECT * FROM \`ORDER\`;                                     | 和保留字、数据库系统或常用方法冲突。语句中使用一对``引起来。 |
| SELECT 'timering' as corporation, last_name<br/>FROM employees; | 在 SELECT 查询结果中增加一列固定的常数列                     |
| SELECT employee_id, last_name, job_id, department_id<br/>FROM employees<br/>WHERE department_id = 90 ; | 过滤数据                                                     |

#### 运算符

| 算术语法                                                     | 作用                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| SELECT A＋B                                                  | + 遇到非数值类型，先尝试转成数值，如果转失败，就按0计算      |
| SELECT A - B                                                 | -                                                            |
| SELECT A * B                                                 | *                                                            |
| SELECT A DIV B<br>SELECT A / B                               | / 一个数除整数，必得浮点（保留4位），除以0为NULL             |
| SELECT A % B<br/>SELECT A MOD B                              | 求模（取余）                                                 |
| **比较语法**                                                 | **作用**                                                     |
| SELECT C FROM TABLE WHERE A = B                              | = 判断等号两边的值、字符串或表达式是否相等。<br/>一个是整数，MySQL会将字符串转化为数字进行比较。如果字符串不能隐式地转为数字，则会等价数字0。<br/>有一个为NULL，结果为NULL。 |
| SELECT C FROM TABLE WHEREA <=> B                             | <=> 安全等于运算符：两个操作数均为NULL时，其返回值为1。<br/>当一个操作数为NULL时，其返回值为0。 |
| SELECT C FROM TABLE WHEREA <> B<br>SELECT C FROM TABLE WHEREA != B | <>OR!= 有任意一个为NULL，结果为NULL。                        |
| SELECT C FROM TABLE WHERE A < B                              | <                                                            |
| SELECT C FROM TABLE WHERE A <= B                             | <=                                                           |
| SELECT C FROM TABLE WHERE A > B                              | >                                                            |
| SELECT C FROM TABLE WHERE A >= B                             | >=                                                           |

#### 非符号类型的运算符

| 语法                                                         | 作用                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| SELECT B FROMTABLE WHERE A IS NULL<br>SELECT B FROM TABLE WHERE A ISNULL | IS NULL 判断是否为空                                         |
| SELECT B FROM TABLE WHERE A IS NOT NULL                      | IS NOT NULL 判断是否非空                                     |
| SELECT D FROM TABLE WHERE C LEAST(A,B)                       | LEAST 返回多值中最小值，字符串时返回字母表中顺序最靠前的字符，有NULL返回NULL |
| SELECT D FROM TABLE WHERE C GREATEST(A,B)                    | GREATEST 返回多值中最大值，字符串时返回字母表中顺序最靠后的字符，有NULL返回NULL |
| SELECT D FROM TABLE WHERE C BETWEEN A AND B                  | 是否在两值之间（闭区间）                                     |
| SELECT D FROMTABLE WHERE C IN (A,B)                          | 是否为列表中任意一个值，有NULL返回NULL                       |
| SELECT D FROM TABLE WHERE C NOT IN (A,B)                     | 是否不为列表中任意一个值                                     |
| SELECT C FROMTABLE WHERE A LIKE '_a%k%'                      | 模糊匹配。“%”：匹配0个或多个字符。<br/>“_”：只能匹配一个字符。`\`表示转义或者`ESCAPE`转义 |
| SELECT C FROM TABLE WHERE A REGEXP 'e$'                      | 正则匹配                                                     |
| SELECT C FROM TABLE WHERE A RLIKE B                          | 正则匹配                                                     |

#### 逻辑运算符

| 语法                             | 作用                                              |
| -------------------------------- | ------------------------------------------------- |
| SELECT NOT A                     | NOT  !                                            |
| SELECT A AND B<br>SELECT A && B  | AND  && 有0返回0，然后再有NULL返回NULL。此外返回1 |
| SELECT A OR B<br/>SELECT A \|\|B | OR 或 优先级1最高，然后是NULL，最后是0            |
| SELECT A XOR B                   | XOR 异或 有NULL返回NULL其他正常                   |

#### 位运算符

位运算符会先将操作数变成二进制数，然后进行位运算，最后将计算结果从二进制变回十进制数。

| 指令          | 作用     |
| ------------- | -------- |
| SELECTA & B   | 按位与   |
| SELECTA \| B  | 按位或   |
| SELECT A ^ B  | 按位异或 |
| SELECT ~ A    | 按位取反 |
| SELECT A >> 2 | 按位右移 |
| SELECT B <<2  | 按位左移 |

#### 优先级运算符

![优先级运算符](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117185303556.png)

#### 正则表达式查询

| 指令       | 作用                                   |
| ---------- | -------------------------------------- |
| '^b'       | 匹配以字母b开头的字符串                |
| 'st$'      | 匹配以 st 结尾的字符串                 |
| 'b.t'      | 匹配任何b和t之间有一个字符的字符串     |
| 'f*n'      | 匹配字符n前面有任意个字符f 的字符串    |
| 'ba+'      | 匹配以b开头后面紧跟至少有一个a的字符串 |
| 'fa'       | 匹配包含fa的字符串                     |
| '[xz]'     | 匹配包含x或者z的字符串                 |
| '\[^abc\]' | 匹配任何不包含a- b或c的字符串          |
| b{2}       | 匹配2个或更多的b                       |
| b{2,4}     | 匹配含最少2个、最多4个b的字符串        |

### MySQL指令

| 指令                                             | 作用                             |
| ------------------------------------------------ | -------------------------------- |
| source d:\xxxx.sql                               | 使用source指令绝对路径导入数据库 |
| DESCRIBE employees;<br/># 或<br/>DESC employees; | 显示表结构                       |

[查看更多](https://github.com/timerring/learn-MySQL/blob/main/SQL%20Cheat%20Sheet.md)



## 致谢

学习参考：MySQL数据库教程 https://www.bilibili.com/video/BV1iq4y1u7vj



## Tips

1. 本仓库针对内容进行了一定程度上的精简，去除了冗余。同时对一些相关的知识进行了适当的补充。
2. 如果您在阅读的过程中存在疑问或发现错误，欢迎提Issues交流订正。
2. 如果遇到图片无法加载的情况，可以考虑使用代理，或者访问[博客网站](https://blog.csdn.net/m0_52316372/category_12173728.html) 。
