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

### 运算符

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

### 非符号类型的运算符

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

### 逻辑运算符

| 语法                             | 作用                                              |
| -------------------------------- | ------------------------------------------------- |
| SELECT NOT A                     | NOT  !                                            |
| SELECT A AND B<br>SELECT A && B  | AND  && 有0返回0，然后再有NULL返回NULL。此外返回1 |
| SELECT A OR B<br/>SELECT A \|\|B | OR 或 优先级1最高，然后是NULL，最后是0            |
| SELECT A XOR B                   | XOR 异或 有NULL返回NULL其他正常                   |

### 位运算符

位运算符会先将操作数变成二进制数，然后进行位运算，最后将计算结果从二进制变回十进制数。

| 指令          | 作用     |
| ------------- | -------- |
| SELECTA & B   | 按位与   |
| SELECTA \| B  | 按位或   |
| SELECT A ^ B  | 按位异或 |
| SELECT ~ A    | 按位取反 |
| SELECT A >> 2 | 按位右移 |
| SELECT B <<2  | 按位左移 |

### 优先级运算符

![优先级运算符](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117185303556.png)

### 正则表达式查询

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

### 排序语法

| 指令                                 | 作用                                                         |
| ------------------------------------ | ------------------------------------------------------------ |
| ORDER BY hire_date DESC;             | 单列排序，ORDER BY 子句在SELECT语句的结尾<br/>ASC（ascend）: 升序（默认）<br>DESC（descend）:降序 |
| ORDER BY department_id, salary DESC; | 可以使用不在SELECT列表中的列排序。<br/>若第一列数据中所有值都是唯一的，将不再对第二列进行排序。 |

### 分页语法

| 指令                                     | 作用                                                         |
| ---------------------------------------- | ------------------------------------------------------------ |
| LIMIT [位置偏移量,] 行数                 | LIMIT 子句必须放在整个 SELECT 语句的最后！<br/>“位置偏移量” 参数指示MySQL从哪一行开始显示（可选参数），默认从第一条记录偏移量为0<br/>“行数”指示返回的记录条数 |
| LIMIT 3 OFFSET 4                         | MySQL 8.0新增，从第5条记录开始后面的3条记录，同`LIMIT 4,3;`  |
| LIMIT (PageNo - 1) * PageSize, PageSize; | 每页参数计算公式，每页的是从第`（当前页数-1）* 每页条数` 条起 |

## 多表查询

| 指令                                                         | 作用                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| SELECT e.last_name,e.salary,j.grade_level<br/>FROM employees e,job_grades j<br/>WHERE e.salary between j.lowest_sal and j.highest_sal; | 等值连接与非等值连接                                         |
| SELECT CONCAT(worker.last_name ,' works for ', manager.last_name)<br/>FROM employees worker, employees manager<br/>WHERE worker.manager_id = manager.employee_id ; | 自连接与非自连接，构造两张表进行匹配                         |
| # 左外连接<br/>SELECT last_name,department_name<br/>FROM employees ,departments<br/>WHERE employees.department_id = departments.department_id(+); | SQL92内连接与外连接，(+) 表示哪个是从表                      |
| SELECT e.last_name, e.department_id, d.department_name<br/>FROM employees e LEFT OUTER JOIN departments d<br/>ON (e.department_id = d.department_id) ; | SQL99内连接与外连接                                          |
| SELECT column,... FROM table1<br/>UNION [ALL]<br/>SELECT column,... FROM table2 | 合并查询结果。UNION 操作符返回两个查询的结果集的并集，去除重复记录。UNION ALL不去重。 |
| SELECT employee_id,last_name,department_name<br/>FROM employees e NATURAL JOIN departments d; | 自然连接，自动查询两张连接表中所有相同的字段，然后进行等值连接。 |
| SELECT employee_id,last_name,department_name<br/>FROM employees e JOIN departments d<br/>USING (department_id); | USING连接。指定数据表里的同名字段进行等值连接。但是只能配合JOIN一起使用。 |

### 7种SQL JOINS的实现

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230119163005000.png)

中图：内连接 A ∩ B

```sql
SELECT employee_id,last_name,department_name
FROM employees e JOIN departments d
ON e.`department_id` = d.`department_id`;
```

左上图：左外连接

```sql
SELECT employee_id,last_name,department_name
FROM employees e LEFT JOIN departments d
ON e.`department_id` = d.`department_id`;
```

右上图：右外连接

```sql
SELECT employee_id,last_name,department_name
FROM employees e RIGHT JOIN departments d
ON e.`department_id` = d.`department_id`;
```

左中图：A - A ∩ B

```sql
SELECT employee_id,last_name,department_name
FROM employees e LEFT JOIN departments d
ON e.`department_id` = d.`department_id`
WHERE d.`department_id` IS NULL
```

右中图：B - A ∩ B

**这里解释一下`WHERE e.department_id IS NULL`，首先是由右外连接衍生出来的，减去中间交集的部分，然后交际的部分是包含A和B的，只需要用条件将 `从表` A置为NULL，即可将在B中有A的部分筛掉。**

```sql
SELECT employee_id,last_name,department_name
FROM employees e RIGHT JOIN departments d
ON e.`department_id` = d.`department_id`
WHERE e.`department_id` IS NULL
```

左下图：满外连接，左中图 + 右上图  A∪B

```sql
SELECT employee_id,last_name,department_name FROM employees e LEFT JOIN departments d
ON e.`department_id` = d.`department_id` WHERE d.`department_id` IS NULL
UNION ALL  #没有去重操作，效率高
SELECT employee_id,last_name,department_name FROM employees e RIGHT JOIN departments d ON e.`department_id` = d.`department_id`;
```

右下图：左中图 + 右中图 A ∪ B - A ∩ B 或者 ( A - A ∩ B) ∪ ( B - A ∩ B）

```sql
SELECT employee_id,last_name,department_name
FROM employees e LEFT JOIN departments d
ON e.`department_id` = d.`department_id`
WHERE d.`department_id` IS NULL
UNION ALL
SELECT employee_id,last_name,department_name
FROM employees e RIGHT JOIN departments d
ON e.`department_id` = d.`department_id`
WHERE e.`department_id` IS NULL
```



## MySQL指令

| 指令                                             | 作用                             |
| ------------------------------------------------ | -------------------------------- |
| source d:\xxxx.sql                               | 使用source指令绝对路径导入数据库 |
| DESCRIBE employees;<br/># 或<br/>DESC employees; | 显示表结构                       |