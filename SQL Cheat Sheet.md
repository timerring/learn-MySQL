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

## 单行函数

### 数值函数

| 函数                | 用法                                                         |
| ------------------- | ------------------------------------------------------------ |
| ABS(x)              | 返回x的绝对值                                                |
| SIGN(X)             | 返回X的符号。正数返回1，负数返回-1，0返回0                   |
| PI()                | 返回圆周率的值                                               |
| CEIL(x)，CEILING(x) | 返回大于或等于某个值的最小整数                               |
| FLOOR(x)            | 返回小于或等于某个值的最大整数                               |
| LEAST(e1,e2,e3…)    | 返回列表中的最小值                                           |
| GREATEST(e1,e2,e3…) | 返回列表中的最大值                                           |
| MOD(x,y)            | 返回X除以Y后的余数                                           |
| RAND()              | 返回0~1的随机值                                              |
| RAND(x)             | 返回0~1的随机值，其中x的值用作种子值，相同的X值会产生相同的随机数 |
| ROUND(x)            | 返回一个对x的值进行四舍五入后，最接近于X的**整数**           |
| ROUND(x,y)          | 返回一个对x的值进行四舍五入后最接近X的值，并保留到小数点后面Y位 |
| TRUNCATE(x,y)       | 返回数字x截断为y位小数的结果                                 |
| SQRT(x)             | 返回x的平方根。当X的值为负数时，返回NULL                     |

### 角度与弧度互换函数

| 函数       | 用法                                  |
| ---------- | ------------------------------------- |
| RADIANS(x) | 将角度转化为弧度，其中，参数x为角度值 |
| DEGREES(x) | 将弧度转化为角度，其中，参数x为弧度值 |

### 三角函数

| 函数       | 用法                                                         |
| ---------- | ------------------------------------------------------------ |
| SIN(x)     | 返回x的正弦值，其中，参数x为弧度值                           |
| ASIN(x)    | 返回x的反正弦值，即获取正弦为x的值。如果x的值不在-1到1之间，则返回NULL |
| COS(x)     | 返回x的余弦值，其中，参数x为弧度值                           |
| ACOS(x)    | 返回x的反余弦值，即获取余弦为x的值。如果x的值不在-1到1之间，则返回NULL |
| TAN(x)     | 返回x的正切值，其中，参数x为弧度值                           |
| ATAN(x)    | 返回x的反正切值，即返回正切值为x的值                         |
| ATAN2(m,n) | 返回两个参数的反正切值                                       |
| COT(x)     | 返回x的余切值，其中，X为弧度值                               |

### 指数与对数

| 函数                 | 用法                                                 |
| -------------------- | ---------------------------------------------------- |
| POW(x,y)，POWER(X,Y) | 返回x的y次方                                         |
| EXP(X)               | 返回e的X次方，其中e是一个常数，2.718281828459045     |
| LN(X)，LOG(X)        | 返回以e为底的X的对数，当X <= 0 时，返回的结果为NULL  |
| LOG10(X)             | 返回以10为底的X的对数，当X <= 0 时，返回的结果为NULL |
| LOG2(X)              | 返回以2为底的X的对数，当X <= 0 时，返回NULL          |

### 进制间的转换

| 函数          | 用法                     |
| ------------- | ------------------------ |
| BIN(x)        | 返回x的二进制编码        |
| HEX(x)        | 返回x的十六进制编码      |
| OCT(x)        | 返回x的八进制编码        |
| CONV(x,f1,f2) | 返回f1进制数变成f2进制数 |

### 字符串函数

| 函数                             | 用法                                                         |
| -------------------------------- | ------------------------------------------------------------ |
| ASCII(S)                         | 返回字符串S中的第一个字符的ASCII码值                         |
| CHAR_LENGTH(s)                   | 返回字符串s的字符数。作用CHARACTER_LENGTH(s)相同             |
| LENGTH(s)                        | 返回字符串s的字节数，和字符集有关                            |
| CONCAT(s1,s2,......,sn)          | 连接s1,s2,......,sn为一个字符串                              |
| CONCAT_WS(x,s1,s2,......,sn)     | 同CONCAT(s1,s2,...)函数，但是每个字符串之间要加上x           |
| INSERT(str, idx, len,replacestr) | 将字符串str从第idx位置开始(1开始)，len个字符长的子串替换为字符replacestr |
| REPLACE(str, a, b)               | 用字符串b替换字符串str中所有出现的字符串a                    |
| UPPER(s)或 UCASE(s)              | 将字符串s的所有字母转成大写字母                              |
| LOWER(s) 或LCASE(s)              | 将字符串s的所有字母转成小写字母                              |
| LEFT(str,n)                      | 返回字符串str最左边的n个字符                                 |
| RIGHT(str,n)                     | 返回字符串str最右边的n个字符                                 |
| LPAD(str, len, pad)              | 用字符串pad对str最左边进行填充，直到str的长度为len个字符     |
| RPAD(str ,len, pad)              | 用字符串pad对str最右边进行填充，直到str的长度为len个字符     |
| LTRIM(s)                         | 去掉字符串s左侧的空格                                        |
| RTRIM(s)                         | 去掉字符串s右侧的空格                                        |
| TRIM(s)                          | 去掉字符串s开始与结尾的空格                                  |
| TRIM(s1 FROM s)                  | 去掉字符串s开始与结尾的s1                                    |
| TRIM(LEADING s1 FROM s)          | 去掉字符串s开始处的s1                                        |
| TRIM(TRAILING s1 FROM s)         | 去掉字符串s结尾处的s1                                        |
| REPEAT(str, n)                   | 返回str重复n次的结果                                         |
| SPACE(n)                         | 返回n个空格                                                  |
| STRCMP(s1,s2)                    | 比较字符串s1,s2的ASCII码值的大小                             |
| SUBSTR(s,index,len)              | 返回从字符串s的index位置其len个字符，作用与SUBSTRING(s,n,len)、MID(s,n,len)相同 |
| LOCATE(substr,str)               | 返回字符串substr在字符串str中首次出现的位置，作用于POSITION(substr IN str)、INSTR(str,substr)相同。未找到，返回0 |
| ELT(m,s1,s2,…,sn)                | 返回指定位置的字符串，如果m=1，则返回s1，如果m=2，则返回s2，如果m=n，则返回sn |
| FIELD(s,s1,s2,…,sn)              | 返回字符串s在字符串列表中第一次出现的位置                    |
| FIND_IN_SET(s1,s2)               | 返回字符串s1在字符串s2中出现的位置。其中，字符串s2是一个以逗号分隔的字符串 |
| REVERSE(s)                       | 返回s反转后的字符串                                          |
| NULLIF(value1,value2)            | 比较两个字符串，如果value1与value2相等，则返回NULL，否则返回value1 |

### 获取日期、时间

| 函数                                                         | 函数                           |
| ------------------------------------------------------------ | ------------------------------ |
| **CURDATE()** ，CURRENT_DATE()                               | 返回当前日期，只包含年、日     |
| **CURTIME()** ， CURRENT_TIME()                              | 返回当前时间，只包含时、分、秒 |
| **NOW()** / SYSDATE() / CURRENT_TIMESTAMP() / LOCALTIME() /LOCALTIMESTAMP() | 返回当前系统日期和时间         |
| UTC_DATE()                                                   | 返回UTC（世界标准时间）日期    |
| UTC_TIME()                                                   | 返回UTC（世界标准时间）时间    |

### 日期与时间戳的转换

| 函数                     | 函数                                                         |
| ------------------------ | ------------------------------------------------------------ |
| UNIX_TIMESTAMP()         | 以UNIX时间戳的形式返回当前时间。SELECT UNIX_TIMESTAMP() - >1634348884 |
| UNIX_TIMESTAMP(date)     | 将时间date以UNIX时间戳的形式返回。                           |
| FROM_UNIXTIME(timestamp) | 将UNIX时间戳的时间转换为普通格式的时间                       |

### 获取月份、星期、星期数、天数等函数

| 函数                                     | 用法                                            |
| ---------------------------------------- | ----------------------------------------------- |
| YEAR(date) / MONTH(date) / DAY(date)     | 返回具体的日期值                                |
| HOUR(time) / MINUTE(time) / SECOND(time) | 返回具体的时间值                                |
| MONTHNAME(date)                          | 返回月份：January，...                          |
| DAYNAME(date)                            | 返回星期几：MONDAY，TUESDAY.....SUNDAY          |
| WEEKDAY(date)                            | 返回周几，注意，周1是0，周2是1，。。。周日是6   |
| QUARTER(date)                            | 返回日期对应的季度，范围为1～4                  |
| WEEK(date) ， WEEKOFYEAR(date)           | 返回一年中的第几周                              |
| DAYOFYEAR(date)                          | 返回日期是一年中的第几天                        |
| DAYOFMONTH(date)                         | 返回日期位于所在月份的第几天                    |
| DAYOFWEEK(date)                          | 返回周几，注意：周日是1，周一是2，。。。周六是7 |

### 日期的操作函数

| 函数                    | 用法                                       |
| ----------------------- | ------------------------------------------ |
| EXTRACT(type FROM date) | 返回指定日期中特定的部分，type指定返回的值 |

### 时间和秒钟转换的函数

| 函数                 | 用法                                                         |
| -------------------- | ------------------------------------------------------------ |
| TIME_TO_SEC(time)    | 将 time 转化为秒并返回结果值。转化的公式为： `小时 *3600+分钟 *60+秒` |
| SEC_TO_TIME(seconds) | 将 seconds 描述转化为包含小时、分钟和秒的时间                |

### 计算日期和时间的函数

| 函数                                                         | 用法                                           |
| ------------------------------------------------------------ | ---------------------------------------------- |
| DATE_ADD(datetime, INTERVAL expr type)，ADDDATE(date,INTERVAL expr type) | 返回与给定日期时间相差INTERVAL时间段的日期时间 |
| DATE_SUB(date,INTERVAL expr type)，SUBDATE(date,INTERVAL expr type) | 返回与date相差INTERVAL时间间隔的日期           |

| 函数                         | 用法                                                         |
| ---------------------------- | ------------------------------------------------------------ |
| ADDTIME(time1,time2)         | 返回time1加上time2的时间。当time2为一个数字时，代表的是秒，可以为负数 |
| SUBTIME(time1,time2)         | 返回time1减去time2后的时间。当time2为一个数字时，代表的是秒，可以为负数 |
| DATEDIFF(date1,date2)        | 返回date1 - date2的日期间隔天数                              |
| TIMEDIFF(time1, time2)       | 返回time1 - time2的时间间隔                                  |
| FROM_DAYS(N)                 | 返回从0000年1月1日起，N天以后的日期                          |
| TO_DAYS(date)                | 返回日期date距离0000年1月1日的天数                           |
| LAST_DAY(date)               | 返回date所在月份的最后一天的日期                             |
| MAKEDATE(year,n)             | 针对给定年份与所在年份中的天数返回一个日期                   |
| MAKETIME(hour,minute,second) | 将给定的小时、分钟和秒组合成时间并返回                       |
| PERIOD_ADD(time,n)           | 返回time加上n后的时间                                        |

### 日期的格式化与解析

| 函数                              | 用法                                       |
| --------------------------------- | ------------------------------------------ |
| DATE_FORMAT(date,fmt)             | 按照字符串fmt格式化日期date值              |
| TIME_FORMAT(time,fmt)             | 按照字符串fmt格式化时间time值              |
| GET_FORMAT(date_type,format_type) | 返回日期字符串的显示格式                   |
| STR_TO_DATE(str, fmt)             | 按照字符串fmt对str进行解析，解析为一个日期 |

| 格式符 | 说明                                                        | 格式符 | 说明                                                        |
| ------ | ----------------------------------------------------------- | ------ | ----------------------------------------------------------- |
| %Y     | 4位数字表示年份                                             | %y     | 表示两位数字表示年份                                        |
| %M     | 月名表示月份（January,....）                                | %m     | 两位数字表示月份（01,02,03...）                             |
| %b     | 缩写的月名（Jan.，Feb.，....）                              | %c     | 数字表示月份（1,2,3,...）                                   |
| %D     | 英文后缀表示月中的天数（1st,2nd,3rd,...）                   | %d     | 两位数字表示月中的天数(01,02...)                            |
| %e     | 数字形式表示月中的天数（1,2,3,4,5.....）                    |        |                                                             |
| %H     | 两位数字表示小数，24小时制（01,02..）                       | %h和%I | 两位数字表示小时，12小时制（01,02..）                       |
| %k     | 数字形式的小时，24小时制(1,2,3)                             | %l     | 数字形式表示小时，12小时制（1,2,3,4....）                   |
| %i     | 两位数字表示分钟（00,01,02）                                | %S和%s | 两位数字表示秒(00,01,02...)                                 |
| %W     | 一周中的星期名称（Sunday...）                               | %a     | 一周中的星期缩写（Sun.，Mon.,Tues.，..）                    |
| %w     | 以数字表示周中的天数(0=Sunday,1=Monday....)                 |        |                                                             |
| %j     | 以3位数字表示年中的天数(001,002...)                         | %U     | 以数字表示年中的第几周，（1,2,3。。）其中Sunday为周中第一天 |
| %u     | 以数字表示年中的第几周，（1,2,3。。）其中Monday为周中第一天 |        |                                                             |
| %T     | 24小时制                                                    | %r     | 12小时制                                                    |
| %p     | AM或PM                                                      | %%     | 表示%                                                       |

### 流程控制函数

| 函数                                                         | 说明                                            |
| ------------------------------------------------------------ | ----------------------------------------------- |
| IF(value,value1,value2)                                      | 如果value的值为TRUE，返回value1，否则返回value2 |
| IFNULL(value1, value2)                                       | 如果value1不为NULL，返回value1，否则返回value2  |
| CASE WHEN 条件1 THEN 结果1 WHEN 条件2 THEN 结果2 .... [ELSE resultn] END | 相当于Java的if...else if...else...              |
| CASE expr WHEN 常量值1 THEN 值1 WHEN 常量值1 THEN 值1 .... [ELSE 值n] END | 相当于Java的switch...case...                    |

### 加密与解密函数

| 函数                        | 用法                                                         |
| --------------------------- | ------------------------------------------------------------ |
| PASSWORD(str)               | 返回字符串str的加密版本，41位长的字符串。加密结果不可逆，常用于用户的密码加密。PASSWORD()在mysql8.0中弃用。 |
| MD5(str)                    | 返回字符串str的md5加密后的值，也是一种加密方式。若参数为NULL，则会返回NULL |
| SHA(str)                    | 从原明文密码str计算并返回加密后的密码字符串，当参数为NULL时，返回NULL。SHA加密算法比MD5更加安全。 |
| ENCODE(value,password_seed) | 返回使用password_seed作为加密密码加密value。mysql8.0中弃用。 |
| DECODE(value,password_seed) | 返回使用password_seed作为加密密码解密value。mysql8.0中弃用。 |

### MySQL信息函数

| 函数                                                  | 用法                                                      |
| ----------------------------------------------------- | --------------------------------------------------------- |
| VERSION()                                             | 返回当前MySQL的版本号                                     |
| CONNECTION_ID()                                       | 返回当前MySQL服务器的连接数                               |
| DATABASE()，SCHEMA()                                  | 返回MySQL命令行当前所在的数据库                           |
| USER()，CURRENT_USER()、SYSTEM_USER()，SESSION_USER() | 返回当前连接MySQL的用户名，返回结果格式为 “主机名@用户名” |
| CHARSET(value)                                        | 返回字符串value自变量的字符集                             |
| COLLATION(value)                                      | 返回字符串value的比较规则                                 |

### 其他函数

| 函数                           | 用法                                                         |
| ------------------------------ | ------------------------------------------------------------ |
| FORMAT(value,n)                | 返回对数字value进行格式化后的结果数据。n表示四舍五入后保留到小数点后n位。 |
| CONV(value,from,to)            | 将value的值进行不同进制之间的转换                            |
| INET_ATON(ipvalue)             | 将以点分隔的IP地址转化为一个数字                             |
| INET_NTOA(value)               | 将数字形式的IP地址转化为以点分隔的IP地址                     |
| BENCHMARK(n,expr)              | 将表达式expr重复执行n次。用于测试MySQL处理expr表达式所耗费的时间 |
| CONVERT(value USING char_code) | 将value所使用的字符编码修改为char_code                       |



## MySQL指令

| 指令                                             | 作用                             |
| ------------------------------------------------ | -------------------------------- |
| source d:\xxxx.sql                               | 使用source指令绝对路径导入数据库 |
| DESCRIBE employees;<br/># 或<br/>DESC employees; | 显示表结构                       |