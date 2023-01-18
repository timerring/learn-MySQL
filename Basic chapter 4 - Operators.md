- [Basic chapter 4 - 运算符](#basic-chapter-4---运算符)
  - [1. 算术运算符](#1-算术运算符)
    - [加法与减法运算符](#加法与减法运算符)
    - [乘法与除法运算符](#乘法与除法运算符)
    - [求模（求余）运算符](#求模求余运算符)
  - [2. 比较运算符](#2-比较运算符)
    - [等号运算符](#等号运算符)
    - [安全等于运算符](#安全等于运算符)
    - [不等于运算符](#不等于运算符)
  - [非符号类型的运算符](#非符号类型的运算符)
    - [空运算符](#空运算符)
    - [非空运算符](#非空运算符)
    - [最小值运算符](#最小值运算符)
    - [最大值运算符](#最大值运算符)
    - [BETWEEN AND运算符](#between-and运算符)
    - [IN运算符](#in运算符)
    - [NOT IN运算符](#not-in运算符)
    - [LIKE运算符](#like运算符)
      - [ESCAPE](#escape)
    - [REGEXP运算符](#regexp运算符)
  - [3. 逻辑运算符](#3-逻辑运算符)
    - [逻辑非运算符](#逻辑非运算符)
    - [逻辑与运算符](#逻辑与运算符)
    - [逻辑或运算符](#逻辑或运算符)
    - [逻辑异或运算符](#逻辑异或运算符)
  - [4. 位运算符](#4-位运算符)
    - [按位与运算符](#按位与运算符)
    - [按位或运算符](#按位或运算符)
    - [按位异或运算符](#按位异或运算符)
    - [按位取反运算符](#按位取反运算符)
    - [按位右移运算符](#按位右移运算符)
    - [按位左移运算符](#按位左移运算符)
  - [5. 运算符的优先级](#5-运算符的优先级)
  - [拓展：使用正则表达式查询](#拓展使用正则表达式查询)
    - [查询以特定字符或字符串开头的记录](#查询以特定字符或字符串开头的记录)
    - [查询以特定字符或字符串结尾的记录](#查询以特定字符或字符串结尾的记录)
    - [用符号"."来替代字符串中的任意一个字符](#用符号来替代字符串中的任意一个字符)
    - [使用"\*"和"+"来匹配多个字符](#使用和来匹配多个字符)
    - [匹配指定字符串](#匹配指定字符串)
    - [匹配指定字符中的任意一个](#匹配指定字符中的任意一个)
    - [匹配指定字符以外的字符](#匹配指定字符以外的字符)
    - [使用{n,}或者{n,m}来指定字符串连续出现的次数](#使用n或者nm来指定字符串连续出现的次数)
  - [练习题](#练习题)


# Basic chapter 4 - 运算符

## 1. 算术运算符

算术运算符主要用于数学运算，其可以连接运算符前后的两个数值或表达式，对数值或表达式进行加（+）、减（-）、乘（*）、除（/）和取模（%）运算。

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117145443485.png)

### 加法与减法运算符

```sql
SELECT 100, 100 + 0, 100 - 0, 100 + 50, 100 + 50 -30, 100 + 35.5, 100 - 35.5
FROM dual;
```

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117153451262.png)

+ 在Java中，+的左右两边如果有字符串，那么表示字符串的拼接。但是在MySQL中+只表示数值相加。如果遇到非数值类型，先尝试转成数值，如果转失败，就按0计算。
+ MySQL 中字符串拼接要使用字符串函数 CONCAT() 实现

### 乘法与除法运算符

```sql
SELECT 100, 100 * 1, 100 * 1.0, 100 / 1.0, 100 / 2,100 + 2 * 5 / 2,100 /3, 100 DIV 0 FROM dual;
```

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117153341733.png)

+ **一个数除以整数后，不管是否能除尽，结果都为一个浮点数；**
+ 一个数除以另一个数，除不尽时，结果为一个浮点数，并保留到**小数点后4位**；
+ 在数学运算中，0不能用作除数，在MySQL中，**一个数除以0为NULL**。

### 求模（求余）运算符

将t22表中的字段i对3和5进行求模（求余）运算。

```sql
SELECT 12 % 3, 12 MOD 5 FROM dual;
```

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117153600811.png)

> 案例：
>
> ```sql
> #筛选出employee_id是偶数的员工
> SELECT * FROM employees
> WHERE employee_id MOD 2 = 0;
> ```

## 2. 比较运算符

比较运算符用来对表达式左边的操作数和右边的操作数进行比较，比较的结果为真则返回1，比较的结果为假则返回0，其他情况则返回NULL。

比较运算符经常被用来作为SELECT查询语句的条件来使用，返回符合条件的结果记录。

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117153736780.png)

### 等号运算符

+ 等号运算符（=）判断等号两边的值、字符串或表达式是否相等，如果相等则返回1，不相等则返回 0。
+ 在使用等号运算符时，遵循如下规则：
  + 如果等号两边的值、字符串或表达式都为字符串，则MySQL会按照字符串进行比较，其比较的是每个字符串中字符的ANSI编码是否相等。
  + 如果等号两边的值都是整数，则MySQL会按照整数来比较两个值的大小。
  + 如果等号两边的值一个是整数，另一个是字符串，则**MySQL会将字符串转化为数字进行比较**。如果字符串不能隐式地转为数字，则会等价数字0。
  + 如果等号两边的值、字符串或表达式中**有一个为NULL，则比较结果为NULL**。

+ 对比：SQL中赋值符号使用 :=

```sql
SELECT 1 = 1, 1 = '1', 1 = 0, 'a' = 'a', (5 + 3) = (2 + 6), '' = NULL , NULL = NULL;
```

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117161047405.png)

### 安全等于运算符 

安全等于运算符（<=>）与等于运算符（=）的作用是相似的， **唯一的区别是‘<=>’可以用来对NULL进行判断**。

+ 在两个操作数均为NULL时，其返回值为1，而不为NULL；
+ 当一个操作数为NULL时，其返回值为0，而不为NULL。

```sql
SELECT 1 <=> '1', 1 <=> 0, 'a' <=> 'a', (5 + 3) <=> (2 + 6), '' <=> NULL,NULL <=> NULL FROM dual;
```

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117165837697.png)

### 不等于运算符

不等于运算符（<>和!=）用于判断两边的数字、字符串或者表达式的值是否不相等.

+ 如果不相等则返回1，相等则返回0。
+ 等于运算符不能判断NULL值。如果两边的值有任意一个为NULL，或两边都为NULL，则结果为NULL。 

SQL语句示例如下：

```sql
SELECT 1 <> 1, 1 != 2, 'a' != 'b', (3+4) <> (2+6), 'a' != NULL, NULL <> NULL;
```

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117170147561.png)

## 非符号类型的运算符

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117170239130.png)

### 空运算符 

空运算符（IS NULL或者ISNULL）判断一个值是否为NULL

+ 如果为NULL则返回1，否则返回0。 

SQL语句示例如下：

```sql
SELECT NULL IS NULL, ISNULL(NULL), ISNULL('a'), 1 IS NULL;
```

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117170548091.png)

> 示例：
>
> ```sql
> #查询commission_pct等于NULL。比较如下的四种写法
> SELECT employee_id,commission_pct FROM employees WHERE commission_pct IS NULL;
> SELECT employee_id,commission_pct FROM employees WHERE commission_pct <=> NULL;
> SELECT employee_id,commission_pct FROM employees WHERE ISNULL(commission_pct);
> ```

### 非空运算符 

非空运算符（IS NOT NULL）判断一个值是否不为NULL。

+ 如果不为NULL则返回1，否则返回0。

SQL语句示例如下：

```sql
SELECT NULL IS NOT NULL, 'a' IS NOT NULL, 1 IS NOT NULL;
```

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117170803954.png)

> 示例：
>
> ```sql
> #查询commission_pct不等于NULL
> SELECT employee_id,commission_pct FROM employees WHERE commission_pct IS NOT NULL;
> SELECT employee_id,commission_pct FROM employees WHERE NOT commission_pct <=> NULL;
> SELECT employee_id,commission_pct FROM employees WHERE NOT ISNULL(commission_pct);
> ```

### 最小值运算符 

语法格式为：LEAST(值1，值2，...，值n)。其中，“值n”表示参数列表中有n个值。在有两个或多个参数的情况下，返回最小值。

+ 当参数是整数或者浮点数时，LEAST将返回其中最小的值；
+ 当参数为字符串时，返回字母表中顺序最靠前的字符；
+ 当比较值列表中有NULL时，不能判断大小，返回值为NULL；

```sql
SELECT LEAST (1,0,2), LEAST('b','a','c'), LEAST(1,NULL,2);
```

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117171107327.png)

由结果可以看到，当参数是整数或者浮点数时，LEAST将返回其中最小的值；当参数为字符串时，返回字母表中顺序最靠前的字符；当比较值列表中有NULL时，不能判断大小，返回值为NULL。

### 最大值运算符

语法格式为：GREATEST(值1，值2，...，值n)。其中，n表示参数列表中有n个值。当有两个或多个参数时，返回值为最大值。

+ 当参数中是整数或者浮点数时，GREATEST将返回其中最大的值；
+ 当参数为字符串时，返回字母表中顺序最靠后的字符；
+ 当比较值列表中有NULL时，不能判断大小，返回值为NULL。

```sql
SELECT GREATEST(1,0,2), GREATEST('b','a','c'), GREATEST(1,NULL,2);
```

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117171315448.png)

### BETWEEN AND运算符

BETWEEN运算符使用的格式通常为SELECT D FROM TABLE WHERE C BETWEEN A AND B，此时，当C大于或等于A，并且C小于或等于B时，结果为1，否则结果为0。**注意是闭区间。**

```sql
SELECT 1 BETWEEN 0 AND 1, 10 BETWEEN 11 AND 12, 'b' BETWEEN 'a' AND 'c';
```

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117171419808.png)

### IN运算符

IN运算符用于判断给定的值是否是IN列表中的一个值。

+ 如果是则返回1，否则返回0。
+ 如果给定的值为NULL，或者IN列表中存在NULL，则结果为NULL。

```sql
SELECT 'a' IN ('a','b','c'), 1 IN (2,3), NULL IN ('a','b'), 'a' IN ('a', NULL);
```

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117172059751.png)

### NOT IN运算符

NOT IN运算符用于判断给定的值是否不是IN列表中的一个值。

+ 如果不是IN列表中的一个值，则返回1，否则返回0。

```sql
SELECT 'a' NOT IN ('a','b','c'), 1 NOT IN (2,3);
```

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117172148177.png)

### LIKE运算符

LIKE运算符主要用来匹配字符串，通常用于模糊匹配。

+ 如果满足条件则返回1，否则返回0。
+ 如果给定的值或者匹配条件为NULL，则返回结果为NULL。

LIKE运算符通常使用如下通配符：

```sql
“%”：匹配0个或多个字符。
“_”：只能匹配一个字符。
```

SQL语句示例如下：

```sql
SELECT NULL LIKE 'abc', 'abc' LIKE NULL;
```

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117172300072.png)

```sql
SELECT first_name
FROM employees
WHERE first_name LIKE 'S%';
```

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117172401853.png)

```sql
SELECT last_name
FROM employees
WHERE last_name LIKE '_o%';
```

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117172422939.png)

#### ESCAPE

回避特殊符号的：使用转义符。例如：将[%]转为[$%]、[]转为[$]，然后再加上[ESCAPE‘$’]即可。

```sql
# 这里采用了\表示转义
SELECT job_id
FROM jobs
WHERE job_id LIKE ‘IT\_%‘;
```

如果使用\表示转义，要省略ESCAPE。如果不是\，则要加上ESCAPE。

```sql
# 这里采用了ESCAPE转义
SELECT job_id
FROM jobs
WHERE job_id LIKE ‘IT$_%‘ escape ‘$‘;
```

### REGEXP运算符

REGEXP运算符用来匹配字符串，语法格式为： expr REGEXP 匹配条件。

+ 如果expr满足匹配条件，返回1；如果不满足，则返回0。
+ 若expr或匹配条件任意一个为NULL，则结果为NULL。

REGEXP运算符在进行匹配时，常用的有下面几种通配符：

```
（1）‘^’匹配以该字符后面的字符开头的字符串。
（2）‘$’匹配以该字符前面的字符结尾的字符串。
（3）‘.’匹配任何一个单字符。
（4）“[...]”匹配在方括号内的任何字符。例如，“[abc]”匹配“a”或“b”或“c”。为了命名字符的范围，使用一
个‘-’。“[a-z]”匹配任何字母，而“[0-9]”匹配任何数字。
（5）‘*’匹配零个或多个在它前面的字符。例如，“x*”匹配任何数量的‘x’字符，“[0-9]*”匹配任何数量的数字，
而“*”匹配任何数量的任何字符。
```

SQL语句示例如下：

```sql
SELECT 'timerring' REGEXP '^t', 'timerring' REGEXP 'g$', 'timerring' REGEXP 'rr';
```

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117183245800.png)

## 3. 逻辑运算符

逻辑运算符主要用来判断表达式的真假，在MySQL中，逻辑运算符的返回结果为1、0或者NULL。

MySQL中支持4种逻辑运算符如下：

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117183359410.png)

### 逻辑非运算符 

逻辑非（NOT或!）运算符表示当给定的值为0时返回1；当给定的值为非0值时返回0；当给定的值为NULL时，返回NULL。

```sql
SELECT NOT 1, NOT 0, NOT(1+1), NOT !1, NOT NULL;
```

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117183448209.png)

> 示例
>
> ```sql
> SELECT last_name, job_id
> FROM employees
> WHERE job_id NOT IN ('IT_PROG', 'ST_CLERK', 'SA_REP');
> ```

### 逻辑与运算符 

逻辑与（AND或&&）运算符是

+ 当给定的所有值均为非0值，并且都不为NULL时，返回1；
+ 当给定的一个值或者多个值为0时则返回0；
+ 否则返回NULL。

```sql
SELECT 1 AND -1, 0 AND 1, 0 AND NULL, 1 AND NULL;
```

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117183645982.png)

### 逻辑或运算符 

逻辑或（OR或||）运算符是

+ 当给定的值都不为NULL，并且任何一个值为非0值时，则返回1，否则返回0；
+ 当一个值为NULL，并且另一个值为非0值时，返回1，
+ 否则返回NULL；当两个值都为NULL时，返回NULL。

```sql
SELECT 1 OR -1, 1 OR 0, 1 OR NULL, 0 || NULL, NULL || NULL;
```

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117183801535.png)

> 示例：
>
> ```sql
> SELECT employee_id, last_name, job_id, salary
> FROM employees
> WHERE salary >= 10000
> OR job_id LIKE '%MAN%';
> ```
>
> 注意：
>
> OR可以和AND一起使用，但是在使用时要注意两者的优先级，由于AND的优先级高于OR，因此先
> 对AND两边的操作数进行操作，再与OR中的操作数结合。

### 逻辑异或运算符

逻辑异或（XOR）运算符是当

+ 给定的值中任意一个值为NULL时，则返回NULL；
+ 如果两个非NULL的值都是0或者都不等于0时，则返回0；
+ 如果一个值为0，另一个值不为0时，则返回1。

```sql
SELECT 1 XOR -1, 1 XOR 0, 0 XOR 0, 1 XOR NULL, 1 XOR 1 XOR 1, 0 XOR 0 XOR 0;
```

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117184155292.png)

> 示例：
>
> ```sql
> select last_name,department_id,salary
> from employees
> where department_id in (10,20) XOR salary > 8000;
> ```

## 4. 位运算符

位运算符是在二进制数上进行计算的运算符。**位运算符会先将操作数变成二进制数，然后进行位运算，最后将计算结果从二进制变回十进制数。**

MySQL支持的位运算符如下：

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117184409426.png)

### 按位与运算符 

按位与（&）运算符将给定值对应的二进制数逐位进行逻辑与运算。

+ 当给定值对应的二进制位的数值都为1时，则该位返回1，否则返回0。

```sql
# 1的二进制数为0001，10的二进制数为1010，所以1 & 10的结果为0000，对应的十进制数为0。
# 20的二进制数为10100，30的二进制数为11110，所以20 & 30的结果为10100，对应的十进制数为20。
SELECT 1 & 10, 20 & 30;
```

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117184534565.png)

### 按位或运算符

按位或（|）运算符将给定的值对应的二进制数逐位进行逻辑或运算。

+ 当给定值对应的二进制位的数值有一个或两个为1时，则该位返回1，否则返回0。

```sql
# 1的二进制数为0001，10的二进制数为1010，所以1 | 10的结果为1011，对应的十进制数为11。
# 20的二进制数为10100，30的二进制数为11110，所以20 | 30的结果为11110，对应的十进制数为30。
SELECT 1 | 10, 20 | 30;
```

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117184641931.png)

### 按位异或运算符

按位异或（^）运算符将给定的值对应的二进制数逐位进行逻辑异或运算。

+ 当给定值对应的二进制位的数值不同时，则该位返回1，否则返回0。

```sql
# 1的二进制数为0001，10的二进制数为1010，所以1 ^ 10的结果为1011，对应的十进制数为11。
# 20的二进制数为10100，30的二进制数为11110，所以20 ^ 30的结果为01010，对应的十进制数为10。
SELECT 1 ^ 10, 20 ^ 30;
```

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117184734745.png)

示例：

```sql
SELECT 12 & 5, 12 | 5,12 ^ 5 FROM DUAL;
```

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117184852969.png)

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117184827831.png)

### 按位取反运算符

按位取反（~）运算符将给定的值的二进制数逐位进行取反操作，即将1变为0，将0变为1。

```sql
# 由于按位取反（~）运算符的优先级高于按位与（&）运算符的优先级，所以10 & ~1，首先，对数字1进行按位取反操作，结果除了最低位为0，其他位都为1，然后与10进行按位与操作，结果为10。
SELECT 10 & ~1;
```

### 按位右移运算符

按位右移（>>）运算符将给定的值的二进制数的所有位右移指定的位数。

+ **右移指定的位数后，右边低位的数值被移出并丢弃，左边高位空出的位置用0补齐。**

```sql
# 1的二进制数为0000 0001，右移2位为0000 0000，对应的十进制数为0。
# 4的二进制数为0000 0100，右移2位为0000 0001，对应的十进制数为1。
SELECT 1 >> 2, 4 >> 2;
```

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117185159053.png)

### 按位左移运算符

按位左移（<<）运算符将给定的值的二进制数的所有位左移指定的位数。左移指定的位数后，左边高位的数值被移出并丢弃，右边低位空出的位置用0补齐。

```sql
SELECT 1 << 2, 4 << 2;
```

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117185231735.png)

## 5. 运算符的优先级

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117185303556.png)

数字编号越大，优先级越高，优先级高的运算符先进行计算。可以看到，赋值运算符的优先级最低，使用“()”括起来的表达式的优先级最高。

## 拓展：使用正则表达式查询

正则表达式通常被用来检索或替换那些符合某个模式的文本内容，根据指定的匹配模式匹配文本中符合要求的特殊字符串。

> 例如，从一个文本文件中提取电话号码，查找一篇文章中重复的单词或者替换用户输入的某些敏感词语等，这些地方都可以使用正则表达式。正则表达式强大而且灵活，可以应用于非常复杂的查询。

MySQL中使用REGEXP关键字指定正则表达式的字符匹配模式。下表列出了REGEXP操作符中常用字符匹配列表。

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230117185441824.png)

### 查询以特定字符或字符串开头的记录

字符‘^’匹配以特定字符或者字符串开头的文本。

> 在fruits表中，查询f_name字段以字母‘b’开头的记录，SQL语句如下：
>
> ```sql
> SELECT * FROM fruits WHERE f_name REGEXP '^b';
> ```

### 查询以特定字符或字符串结尾的记录

字符‘$’匹配以特定字符或者字符串结尾的文本。

> 在fruits表中，查询f_name字段以字母‘y’结尾的记录，SQL语句如下：
>
> ```sql
> SELECT * FROM fruits WHERE f_name REGEXP 'y$';
> ```

### 用符号"."来替代字符串中的任意一个字符

字符‘.’匹配任意一个字符。 在fruits表中，查询f_name字段值

> 包含字母‘a’与‘g’且两个字母之间只有一个字母的记录，SQL语句如下：
>
> ```sql
> SELECT * FROM fruits WHERE f_name REGEXP 'a.g';
> ```

### 使用"*"和"+"来匹配多个字符

星号‘*’匹配前面的字符任意多次，包括0次。加号‘+’匹配前面的字符至少一次。

> 在fruits表中，查询f_name字段值以字母‘b’开头且‘b’后面出现字母‘a’的记录，SQL语句如下：
>
> ```sql
> SELECT * FROM fruits WHERE f_name REGEXP '^ba*'; # 任意多次包括0次
> SELECT * FROM fruits WHERE f_name REGEXP '^ba+'; # 至少一次
> ```

### 匹配指定字符串

正则表达式可以匹配指定字符串，只要这个字符串在查询文本中即可，如要匹配多个字符串，**多个字符串之间使用分隔符‘|’隔开。**

在fruits表中，查询f_name字段值包含字符串“on”的记录，SQL语句如下：

```sql
SELECT * FROM fruits WHERE f_name REGEXP 'on';
```

在fruits表中，查询f_name字段值包含字符串“on”或者“ap”的记录，SQL语句如下：

```sql
SELECT * FROM fruits WHERE f_name REGEXP 'on|ap';
```

之前介绍过，LIKE运算符也可以匹配指定的字符串，

+ 但与REGEXP不同，LIKE匹配的字符串如果在文本中间出现，则找不到它，相应的行也不会返回。
+ REGEXP在文本内进行匹配，如果被匹配的字符串在文本中出现，REGEXP将会找到它，相应的行也会被返回。对比结果如下所示。

在fruits表中，使用LIKE运算符查询f_name字段值为“on”的记录，SQL语句如下：

```sql
SELECT * FROM fruits WHERE f_name like 'on';
# Empty set(0.00 sec)
```

### 匹配指定字符中的任意一个

方括号“[]”指定一个字符集合，只匹配其中任何一个字符，即为所查找的文本。

在fruits表中，查找f_name字段中包含字母‘o’或者‘t’的记录，SQL语句如下：

```sql
SELECT * FROM fruits WHERE f_name REGEXP '[ot]';
```

### 匹配指定字符以外的字符

 “\[^字符集合]” 匹配不在指定集合中的任何字符。

在fruits表中，查询f_id字段中包含字母a~e和数字1~2以外字符的记录，SQL语句如下：

```sql
SELECT * FROM fruits WHERE f_id REGEXP '[^a-e1-2]';
```

### 使用{n,}或者{n,m}来指定字符串连续出现的次数 

“字符串{n,}”表示至少匹配n次前面的字符；“字符串{n,m}”表示匹配前面的字符串不少于n次，不多于m次。

在fruits表中，查询f_name字段值出现字符串“ba”最少1次、最多3次的记录，SQL语句如下：

```sql
SELECT * FROM fruits WHERE f_name REGEXP 'ba{1,3}';
```

## 练习题

1.选择工资不在5000到12000的员工的姓名和工资

```sql
SELECT last_name, salary
FROM employees
WHERE salary NOT BETWEEN 5000 and 12000;
```

2.选择在20或50号部门工作的员工姓名和部门号

```sql
SELECT last_name, department_id
FROM employees
WHERE department_id IN (20, 50);
```

3.选择公司中没有管理者的员工姓名及job_id

```sql
SELECT last_name, job_id
FROM employees
WHERE manager_id IS NULL;
```

4.选择公司中有奖金的员工姓名，工资和奖金级别

```sql
SELECT last_name, salary, commission_pct
FROM employees
WHERE commission_pct IS NOT NULL;
```

5.选员工姓名的第三个字母是a的员工姓名

```sql
SELECT last_name
FROM employees
WHERE last_name LIKE '__a%';
```

6.选择姓名中有字母a和k的员工姓名

```sql
SELECT last_name
FROM employees
WHERE last_name LIKE '%a%k%' OR last_name LIKE '%k%a%';
# 注意这里OR前后要写完整的语句。只写WHERE last_name LIKE '%a%k%' OR LIKE '%k%a%';是错的
```

7.显示出表 employees 表中 first_name 以 'e'结尾的员工信息

```sql
SELECT employee_id,first_name,last_name
FROM employees
WHERE first_name LIKE '%e';
```

```sql
SELECT employee_id,first_name,last_name
FROM employees
WHERE first_name REGEXP 'e$';
```

8.显示出表 employees 部门编号在 80-100 之间的姓名、工种

```sql
SELECT last_name,job_id
FROM employees
WHERE department_id BETWEEN 80 AND 100;
```

9.显示出表 employees 的 manager_id 是 100,101,110 的员工姓名、工资、管理者id

```sql
SELECT last_name,salary, manager_id
FROM employees
WHERE manager_id IN (100, 101, 110);
```



[返回首页](https://github.com/timerring/learn-MySQL)