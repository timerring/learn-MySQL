# learn-MySQL
> Further study and note-taking of MySQL, including principle analysis, practical code, interview questions and SQL cheat sheet.

MySQL的深层学习和笔记，包括原理分析、实用代码、面试题和SQL速查表。

## MySQL 数据库基础篇

[Basic chapter 1 - 数据库概述](https://github.com/timerring/learn-MySQL/blob/main/Basic%20chapter%201%20-%20Database%20Overview.md)

[Basic chapter 2 - MySQL环境搭建](https://github.com/timerring/learn-MySQL/blob/main/Basic%20chapter%202%20-%20MySQL%20Environment%20Setup.md)

[Basic chapter 3 - 基本的SELECT语句](https://github.com/timerring/learn-MySQL/blob/main/Basic%20chapter%203%20-%20Basic%20SELECT%20Statement.md)

## MySQL 数据库高级篇

Coming Soon...



## MySQL 实用代码库

Coming Soon...



## SQL速查表

#### 注释

| 语法           | 作用     |
| -------------- | -------- |
| # 注释文字     | 单行注释 |
| -- 注释文字    | 单行注释 |
| /* 注释文字 */ | 多行注释 |

#### SELECT语句

| 语法                                                         | 作用                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| SELECT 1+1, 2+2 FROM DUAL;                                   | 伪表查询                                                     |
| SELECT department_id, location_id<br/>FROM departments;      | 普通字段查询                                                 |
| SELECT last_name "Name", salary*12 "Annual Salary"<br/>FROM employees; | 列的别名。(列和别名之间加`AS`也行)。                         |
| SELECT DISTINCT department_id<br/>FROM employees;            | 关键字DISTINCT去除重复行                                     |
| SELECT * FROM \`ORDER\`;                                     | 和保留字、数据库系统或常用方法冲突。语句中使用一对``引起来。 |
| SELECT 'timering' as corporation, last_name<br/>FROM employees; | 在 SELECT 查询结果中增加一列固定的常数列                     |
| SELECT employee_id, last_name, job_id, department_id<br/>FROM employees<br/>WHERE department_id = 90 ; | 过滤数据                                                     |

#### MySQL指令

| 指令                                             | 作用                             |
| ------------------------------------------------ | -------------------------------- |
| source d:\xxxx.sql                               | 使用source指令绝对路径导入数据库 |
| DESCRIBE employees;<br/># 或<br/>DESC employees; | 显示表结构                       |

[查看详情](https://github.com/timerring/learn-MySQL/blob/main/SQL%20Cheat%20Sheet.md)



## 致谢

学习参考：MySQL数据库教程 https://www.bilibili.com/video/BV1iq4y1u7vj



## Tips

1. 本仓库针对内容进行了一定程度上的精简，去除了冗余。同时对一些相关的知识进行了适当的补充。
2. 如果您在阅读的过程中存在疑问或发现错误，欢迎提Issues交流订正。
2. 如果遇到图片无法加载的情况，可以考虑使用代理，或者访问[博客网站](https://blog.csdn.net/m0_52316372/category_12173728.html) 。
