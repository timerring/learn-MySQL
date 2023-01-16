# SQL速查表

## 注释

| 语法           | 作用     |
| -------------- | -------- |
| # 注释文字     | 单行注释 |
| -- 注释文字    | 单行注释 |
| /* 注释文字 */ | 多行注释 |

## SELECT语句

| 语法                                                         | 作用                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| SELECT 1+1, 2+2 FROM DUAL;                                   | 伪表查询                                                     |
| SELECT department_id, location_id<br/>FROM departments;      | 普通字段查询                                                 |
| SELECT last_name "Name", salary*12 "Annual Salary"<br/>FROM employees; | 列的别名。(列和别名之间加`AS`也行)。                         |
| SELECT DISTINCT department_id<br/>FROM employees;            | 关键字DISTINCT去除重复行                                     |
| SELECT * FROM \`ORDER\`;                                     | 和保留字、数据库系统或常用方法冲突。语句中使用一对``引起来。 |
| SELECT 'timering' as corporation, last_name<br/>FROM employees; | 在 SELECT 查询结果中增加一列固定的常数列                     |
| SELECT employee_id, last_name, job_id, department_id<br/>FROM employees<br/>WHERE department_id = 90 ; | 过滤数据                                                     |

## MySQL指令

| 指令                                             | 作用                             |
| ------------------------------------------------ | -------------------------------- |
| source d:\xxxx.sql                               | 使用source指令绝对路径导入数据库 |
| DESCRIBE employees;<br/># 或<br/>DESC employees; | 显示表结构                       |