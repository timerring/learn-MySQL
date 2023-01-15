# Basic chapter 2 - MySQL环境搭建

## 1. MySQL的卸载

### 步骤1：停止MySQL服务

打开“任务管理器”，在“服务”列表找到“MySQL8.0”的服务，右键单击服务，选择“停止”选项停止MySQL8.0的服务，如图所示。

> 也可以搜索计算机管理 ----> 服务和应用程序 ----->服务 中可以查看当前正在运行的进程。

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230115111704942.png)

### 步骤2：软件卸载

方式1：通过控制面板方式

卸载MySQL8.0的程序可以和其他桌面应用程序一样直接在“控制面板”选择“卸载程序”，并在程序列表中找到MySQL8.0服务器程序，直接双击卸载即可，如图所示。

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230115111812014.png)

方式2：通过安装包提供的卸载功能卸载

你也可以通过安装向导程序(下载的mysql-installer-community.msi文件)进行MySQL8.0服务器程序的卸载。按照提示操作即可，在卸载过程中，想要同时删除MySQL服务器中的数据，则勾选“Remove the data directory”，想要同时卸载MySQL8.0的安装向导程序，勾选“Yes，Uninstall MySQL Installer” 即可。

### 步骤3：残余文件的清理

对残余文件进行清理即可，主要是两个文件夹，分别是安装目录以及数据存储的目录。

### 步骤4：清理注册表

在系统的搜索框中输入`regedit`。

```
HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Services\Eventlog\Application\MySQL服务 目录删除
HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Services\MySQL服务 目录删除
HKEY_LOCAL_MACHINE\SYSTEM\ControlSet002\Services\Eventlog\Application\MySQL服务 目录删除
HKEY_LOCAL_MACHINE\SYSTEM\ControlSet002\Services\MySQL服务 目录删除
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Eventlog\Application\MySQL服务目录
删除
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MySQL服务删除
```

> 注册表中的ControlSet001, ControlSet002,不一定是001和002,可能是ControlSet005、006之类

### 步骤5：删除环境变量配置

找到path环境变量，将其中关于`mysql`的环境变量删除。

## 2. MySQL的下载、安装、配置

### MySQL的4大版本

+ MySQL Community Server 社区版本，开源免费，自由下载，但不提供官方技术支持，适用于大多数普通用户。
+ MySQL Enterprise Edition 企业版本，需付费，不能在线下载，可以试用30天。提供了更多的功能和更完备的技术支持，更适合于对数据库的功能和可靠性要求较高的企业客户。
+ MySQL Cluster 集群版，开源免费。用于架设集群服务器，可将几个MySQL Server封装成一个Server。需要在社区版或企业版的基础上使用。
+ MySQL Cluster CGE 高级集群版，需付费。

### 软件的下载

下载地址 官网： https://www.mysql.com

打开官网，点击DOWNLOADS，然后，点击 MySQL Community(GPL) Downloads

![image-20230115112959956](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230115112959956.png)

点击 MySQL Community Server

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230115113110760.png)

在General Availability(GA) Releases中选择适合的版本

Windows平台下提供两种安装文件：MySQL二进制分发版（.msi安装文件）和免安装版（.zip压缩文
件）。一般来讲，应当使用二进制分发版，因为该版本提供了图形化的安装向导过程。

这里在Windows 系统下推荐下载MSI安装程序；点击Go to Download Page 进行下载即可

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230115113152810.png)

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230115113218589.png)

区别：

+ mysql-installer-web-community-8.0.26.0.msi 下载程序大小：2.4M；安装时需要**联网安装组件**。
+ mysql-installer-community-8.0.26.0.msi 下载程序大小：450.7M；安装时**离线安装**即可。

如果安装MySQL5.7版本的话，选择`Archives` ，接着选择MySQL5.7的相应版本。

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230115113343060.png)

### MySQL8.0 版本的安装

步骤1：双击下载的.msi文件，打开安装向导。

步骤2：打开“Choosing a Setup Type”（选择安装类型）窗口，在其中列出了5种安装类型，分别是
Developer Default（默认安装类型）、Server only（仅作为服务器）、Client only（仅作为客户端）、
Full（完全安装）、Custom（自定义安装）。这里选择“`Custom`（自定义安装）”类型按钮，单击“Next(下
一步)”按钮。

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230115113527056.png)

步骤3：打开“Select Products” （选择产品）窗口，可以定制需要安装的产品清单。例如，选择“MySQL
Server 8.0.26-X64”后，单击“→”添加按钮，即可选择安装MySQL服务器。

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230115113541999.png)

此时如果直接“Next”（下一步），则产品的安装路径是默认的。如果想要自定义安装目录，则可以选中
对应的产品，然后在下面会出现“Advanced Options”（高级选项）的超链接。

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230115113630534.png)

单击“Advanced Options”（高级选项）则会弹出安装目录的选择窗口，如图所示，此时你可以分别设置
MySQL的服务程序安装目录和数据存储目录。**如果不设置，默认分别在C盘的Program Files目录和**
**ProgramData目录（这是一个隐藏目录）。**如果自定义安装目录，建议服务目录和数据目录分开存放。

步骤4：在上一步选择好要安装的产品之后，单击“Next”（下一步）进入确认窗口，如图所示。单击“Execute”（执行）按钮开始安装。

步骤5：安装完成后在“Status”（状态）列表下将显示“Complete”（安装完成），如图所示。

### 配置MySQL8.0

MySQL安装之后，需要对服务器进行配置。具体的配置步骤如下。

步骤1：在上一个小节的最后一步，单击“Next”（下一步）按钮，就可以进入产品配置窗口。

步骤2：单击“Next”（下一步）按钮，进入MySQL服务器类型配置窗口，如图所示。端口号一般选择默认
端口号3306。

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230115113913184.png)

其中，“Config Type”选项用于设置服务器的类型。单击该选项右侧的下三角按钮，即可查看3个选项。

+ `Development Machine（开发机器）` ：该选项代表典型个人用桌面工作站。此时机器上需要运行多个应用程序，那么MySQL服务器将占用最少的系统资源。
+ `Server Machine（服务器）` ：该选项代表服务器，MySQL服务器可以同其他服务器应用程序一起运行，例如Web服务器等。MySQL服务器配置成适当比例的系统资源。
+ `Dedicated Machine（专用服务器）` ：该选项代表只运行MySQL服务的服务器。MySQL服务器配置成使用所有可用系统资源。

步骤3：单击“Next”（下一步）按钮，打开设置授权方式窗口。其中，上面的选项是MySQL8.0提供的新的
授权方式，采用SHA256基础的密码加密方法；下面的选项是传统授权方法（保留5.x版本兼容性）。

步骤4：单击“Next”（下一步）按钮，打开设置服务器root超级管理员的密码窗口，如图所示，需要输入
两次同样的登录密码。也可以通过“Add User”添加其他用户，添加其他用户时，需要指定用户名、允许
该用户名在哪台/哪些主机上登录，还可以指定用户角色等。此处暂不添加用户。

步骤5：单击“Next”（下一步）按钮，打开设置服务器名称窗口，如图所示。该服务名会出现在Windows
服务列表中，也可以在命令行窗口中使用该服务名进行启动和停止服务。本书将服务名设置为
“MySQL80”。如果希望开机自启动服务，勾选“Start the MySQL Server at System Startup”选项。

下面是选择以什么方式运行服务？可以选择“Standard System Account”(标准系统用户)或者“Custom User”
(自定义用户)中的一个。这里推荐前者。

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230115114226613.png)

步骤6：单击“Next”（下一步）按钮，打开确认设置服务器窗口，单击“Execute”（执行）按钮。

步骤7：完成配置。单击“Finish”（完成）按钮，即可完成服务器的配置。

### 配置MySQL8.0 环境变量

> **软件的`bin`目录放在`path`环境下，可以达到在任意目录下都可以运行软件的目的。**

如果不配置MySQL环境变量，就不能在命令行直接输入MySQL登录命令。下面说如何配置MySQL的环境
变量：

步骤1：在桌面上右击【此电脑】图标，在弹出的快捷菜单中选择【属性】菜单命令。 

步骤2：打开【系统】窗口，单击【高级系统设置】链接。 

步骤3：打开【系统属性】对话框，选择【高级】选项卡，然后单击【环境变量】按钮。

步骤4：打开【环境变量】对话框，在系统变量列表中选择path变量。 

步骤5：单击【编辑】按钮，在【编辑环境变量】对话框中，将MySQL应用程序的bin目录添加到变量值中，用分号将其与其他路径分隔开。注意是**系统变量**中的path。

步骤6：添加完成之后，单击【确定】按钮，这样就完成了配置path变量的操作，然后就可以直接输入MySQL命令来登录数据库了。

### MySQL5.7 版本的安装、配置

安装过程基本同8.0，这里不赘述。配置MySQL5.7时，**一定与前面安装好的MySQL8.0不能使用相同的端口号。**在1-65535($2^{16}$)之间。此外注意，**在安装两个版本的SQL之后，就不需要再添加环境变量path了，因为这两个谁在上面就先运行谁的。添加两个path没有实际的作用**。

> 这里补充有关单机端口号上限的问题：
>
> 单机端口号上限为 65536，其中系统默认对外连接可用的端口号范围为 32768-61000，这个范围可以修改，但因为小于 1024 的端口号一方面属于知名端口，另一方面默认只能 root权限使用，故可用端口号范围最大设置到 1024-65535，这意味着单个IP同一时间对外建立连接的最大连接数是 64511。

### 安装失败问题

**问题1：无法打开MySQL8.0软件安装包或者安装过程中失败，如何解决？**

在运行MySQL8.0软件安装包之前，用户需要确保系统中已经安装了.Net Framework相关软件，如果缺少
此软件，将不能正常地安装MySQL8.0软件。

解决方案：到这个地址https://www.microsoft.com/en-us/download/details.aspx?id=42642 下载Microsoft
.NET Framework 4.5并安装后，再去安装MySQL。

另外，还要确保Windows Installer正常安装。windows上安装mysql8.0需要操作系统提前已安装好
Microsoft Visual C++ 2015-2019。

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230115115126261.png)

解决方案同样是，提前到微软官网https://support.microsoft.com/en-us/topic/the-latest-supported-visual-c-downloads-2647da03-1eea-4433-9aff-95f26a218cc0 ，下载相应的环境。

**问题2：卸载重装MySQL失败？**

该问题通常是因为MySQL卸载时，没有完全清除相关信息导致的。

解决办法是，把以前的安装目录删除。如果之前安装并未单独指定过服务安装目录，则默认安装目录是
“C:\Program Files\MySQL”，彻底删除该目录。同时删除MySQL的Data目录，如果之前安装并未单独指定
过数据目录，则默认安装目录是“C:\ProgramData\MySQL”，该目录一般为隐藏目录。删除后，重新安装
即可。

**问题3：如何在Windows系统删除之前的未卸载干净的MySQL服务列表？**

操作方法如下，在系统“搜索框”中输入“cmd”，按“Enter”（回车）键确认，弹出命令提示符界面。然后输
入“sc delete MySQL服务名”,按“Enter”（回车）键，就能彻底删除残余的MySQL服务了。

## 3. MySQL的登录

### 服务的启动与停止

**MySQL安装完毕之后，需要启动服务器进程，不然客户端无法连接数据库。**

在前面的配置过程中，已经将MySQL安装为Windows服务，并且勾选当Windows启动、停止时，MySQL也
自动启动、停止。

方式1：在windows服务中启动或者停止。

方式2：使用命令行，注意要使用**系统管理员身份**打开。

```bash
# 启动 MySQL 服务命令：
net start MySQL服务名

# 停止 MySQL 服务命令：
net stop MySQL服务名
```

这里以服务MySQL80为例：

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230115121508755.png)

### 自带客户端的登录与退出

MySQL服务启动完成后，可以通过客户端来登录MySQL数据库。

方式1：MySQL自带命令行 (仅限于root用户)

```
所有程序 → MySQL → MySQL 8.0 Command Line Client
```

方式2：windows命令行

格式：

```bash
mysql -h 主机名 -P 端口号 -u 用户名 -p
Enter password:密码
```

举例：

```bash
mysql -h localhost -P 3306 -u root -p
Enter password:****
```

注意：

客户端和服务器在同一台机器上，所以输入localhost或者IP地址127.0.0.1。同时，因为是连接本机： -hlocalhost就可以省略，如果端口号没有修改：-P3306也可以省略。

连接成功后，有关于MySQL Server服务版本的信息，还有第几次连接的id标识。

也可以在命令行通过以下方式获取MySQL Server服务版本的信息：

```bash
mysql --version
# or
mysql -V
```

或登录后，通过以下方式查看当前版本信息：

```bash
select version();
```

退出登录

```bash
exit
# 或
quit
```

## 4. MySQL演示使用

### MySQL的使用演示

#### 1、查看所有的数据库

```sql
show databases;
```

+ “information_schema”是 MySQL 系统自带的数据库，主要保存 MySQL 数据库服务器的系统信息，比如数据库的名称、数据表的名称、字段名称、存取权限、数据文件 所在的文件夹和系统使用的文件夹，等等
+ “performance_schema”是 MySQL 系统自带的数据库，可以用来监控 MySQL 的各类性能指标。
+ “sys”数据库是 MySQL 系统自带的数据库，主要作用是以一种更容易被理解的方式展示 MySQL 数据库服务器的各类性能指标，帮助系统管理员和开发人员监控 MySQL 的技术性能。
+ “mysql”数据库保存了 MySQL 数据库服务器运行时需要的系统信息，比如数据文件夹、当前使用的字符集、约束检查信息，等等

#### 2、创建自己的数据库

```sql
create database 数据库名;
#创建timerring数据库，该名称不能与已经存在的数据库重名。
create database timerring;
```

#### 3、使用自己的数据库

```sql
use 数据库名;
#使用timerring数据库
use timerring;
```

说明：如果没有使用use语句，后面针对数据库的操作也没有加“数据名”的限定，那么会报“ERROR 1046
(3D000): No database selected”（没有选择数据库）

使用完use语句之后，如果接下来的SQL都是针对一个数据库操作的，那就不用重复use了，如果要针对另
一个数据库操作，那么要重新use。

#### 4、查看某个库的所有表格

```sql
show tables; #要求前面有use语句

show tables from 数据库名;
```

#### 5、创建新的表格

```sql
create table 表名称(
字段名 数据类型,
字段名 数据类型
);
```

说明：如果是最后一个字段，后面就用加逗号，因为逗号的作用是分割每个字段。

```sql
#创建学生表
create table student(
id int,
name varchar(20) #说名字最长不超过20个字符
);
```

#### 6、查看一个表的数据

```sql
select * from 数据库表名称;
```

#### 7、添加一条记录

```sql
insert into 表名称 values(值列表);
# 添加两条记录到student表中
insert into student values(1,'张三');
insert into student values(2,'李四');
```

在5.7及以下的版本中，可能会存在以下报错：

```sql
mysql> insert into student values(1,'张三');
ERROR 1366 (HY000): Incorrect string value: '\xD5\xC5\xC8\xFD' for column 'name' at
row 1
mysql> insert into student values(2,'李四');
ERROR 1366 (HY000): Incorrect string value: '\xC0\xEE\xCB\xC4' for column 'name' at
row 1
mysql> show create table student;
```

这是有关于字符集的问题，下面会给出解决方案。

#### 8、查看表的创建信息

```sql
show create table 表名称\G
```

```sql
#查看student表的详细创建信息
show create table student\G
#结果如下
*************************** 1. row ***************************
Table: student
Create Table: CREATE TABLE `student` (
`id` int(11) DEFAULT NULL,
`name` varchar(20) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=latin1
1 row in set (0.00 sec)
```

上面的结果显示student的表格的默认字符集是“latin1”不支持中文。

#### 9、查看数据库的创建信息

```sql
show create database 数据库名\G
```

```sql
#查看timerring数据库的详细创建信息
show create database timerring\G
#结果如下
*************************** 1. row ***************************
Database: timerring
Create Database: CREATE DATABASE `timerring` /*!40100 DEFAULT CHARACTER SET latin1 */
1 row in set (0.00 sec)
```

上面的结果显示timerring数据库也不支持中文，字符集默认是latin1。

#### 10、删除表格

```sql
drop table 表名称;
```

```sql
#删除学生表
drop table student;
```

#### 11、删除数据库

```sql
drop database 数据库名;
```

```sql
#删除timerring数据库
drop database timerring;
```

### MySQL的编码设置

#### MySQL5.7中

命令行操作sql乱码问题

```sql
ERROR 1366 (HY000): Incorrect string value: '\xD5\xC5\xC8\xFD' for column 'sname' at
row 1
```

问题解决

步骤1：查看编码命令

```sql
show variables like 'character_%';
show variables like 'collation_%';
```

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230115125809866.png)

步骤2：修改mysql的数据目录下的my.ini配置文件

```ini
[mysql] #大概在63行左右，在其下添加
...
default-character-set=utf8 #默认字符集
[mysqld] # 大概在76行左右，在其下添加
...
character-set-server=utf8
collation-server=utf8_general_ci
```

> 注意：建议修改配置文件使用notepad++等高级文本编辑器，使用记事本等软件打开修改后可能会导致文件编码修改为“含BOM头”的编码，从而服务重启失败。

步骤3：重启服务

步骤4：查看编码命令

```sql
show variables like 'character_%';
show variables like 'collation_%';
```

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230115130154539.png)

可见，已经将latin1修改为了utf8。

#### MySQL8.0中

在MySQL 8.0版本之前，默认字符集为latin1，utf8字符集指向的是utf8mb3。网站开发人员在数据库设计的时候往往会将编码修改为utf8字符集。如果遗忘修改默认的编码，就会出现乱码的问题。从MySQL 8.0开始，数据库的默认编码改为utf8mb4 ，从而避免了上述的乱码问题。

## 5. MySQL图形化管理工具

常用的图形化管理工具有：MySQL Workbench、phpMyAdmin、Navicat Preminum、MySQLDumper、SQLyog、dbeaver、MySQL ODBC Connector。

这里重点介绍Navicat软件：

Navicat MySQL是一个强大的MySQL数据库服务器管理和开发工具。它可以与任何3.21或以上版本的
MySQL一起工作，支持触发器、存储过程、函数、事件、视图、管理用户等。图形用户界面（GUI）可以让用户用一种安全简便的方式来快速方便地创建、组织、访问和共享信息。Navicat支持中文，下载地址： http://www.navicat.com/ 。

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230115161159492.png)

输入密码，测试连接正确后，直接连接即可。

可能出现连接问题：

有些图形界面工具，特别是旧版本的图形界面工具，在连接MySQL8时出现“Authentication plugin
'caching_sha2_password' cannot be loaded”错误。

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230115161402892.png)

原因是MySQL8之前的版本中加密规则是mysql_native_password，而在MySQL8之后，加密规则是caching_sha2_password。解决问题方法有两种，第一种是升级图形界面工具版本，第二种是把MySQL8
用户登录密码加密规则还原成mysql_native_password。

下面介绍一下第二种还原的方法：

用命令行登录MySQL数据库之后，执行如下命令修改用户密码加密规则并更新用户密码，这里修改用户为“root@localhost”的用户密码规则为“mysql_native_password”，密码值为“123456”，输入下面命令即可。

```sql
#使用mysql数据库
USE mysql;
#修改'root'@'localhost'用户的密码规则和密码
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'abc123';
#刷新权限
FLUSH PRIVILEGES;
```

## 6. MySQL目录结构与源码

### 主要目录结构

| MySQL的目录结构                             | 说明                                 |
| ------------------------------------------- | ------------------------------------ |
| bin目录                                     | 所有MySQL的可执行文件。如：mysql.exe |
| MySQLInstanceConfig.exe                     | 数据库的配置向导，在安装时出现的内容 |
| data目录                                    | 系统数据库所在的目录                 |
| my.ini文件                                  | MySQL的主要配置文件                  |
| c:\ProgramData\MySQL\MySQL Server 8.0\data\ | 用户创建的数据库所在的目录           |

### MySQL 源代码获取

首先，你要进入 MySQL下载界面。 这里你不要选择用默认的“Microsoft Windows”，而是要通过下拉栏，
找到“Source Code”，在下面的操作系统版本里面， 选择 Windows（Architecture Independent），然后点
击下载。接下来，把下载下来的压缩文件解压，即 MySQL 的源代码，MySQL 是用 C++ 开发而成的。

mysql目录下的各个子目录，包含了 MySQL 各部分组件的源代码，其中

+ sql 子目录是 MySQL 核心代码；
+ libmysql 子目录是客户端程序 API；
+ mysql-test 子目录是测试工具；
+ mysys 子目录是操作系统相关函数和辅助函数；

## 7. 常见问题的解决

**问题1：root用户密码忘记，重置的操作**

1: 通过任务管理器或者服务管理，关掉mysqld(服务进程) 

2: 通过命令行+特殊参数开启mysqld 

```sql
mysqld -- defaults-file="D:\ProgramFiles\mysql\MySQLServer5.7Data\my.ini" --skip-grant-tables
```

3: 此时，mysqld服务进程已经打开。并且不需要权限检查 

4: mysql -uroot 无密码登陆服务器。另启动一个客户端进行 

5: 修改权限表

```sql
use mysql; 

update user set authentication_string=password('新密码') where user='root' and Host='localhost'; 

flush privileges; 
```

6: 通过任务管理器，关掉mysqld服务进程。 

7: 再次通过服务管理，打开mysql服务，即可用修改后的新密码登陆。

**问题2：mysql命令报“不是内部或外部命令”**

如果输入mysql命令报“不是内部或外部命令”，把mysql安装目录的bin目录配置到环境变量path中。

**问题3：错误ERROR ：没有选择数据库就操作表格和数据**

`ERROR 1046 (3D000): No database selected`

+ 解决方案一：就是使用“USE 数据库名;”语句，这样接下来的语句就默认针对这个数据库进行操作
+ 解决方案二：就是所有的表对象前面都加上“数据库.”

**问题4：命令行客户端的字符集问题**

```sql
mysql> INSERT INTO t_stu VALUES(1,'张三','男');
ERROR 1366 (HY000): Incorrect string value: '\xD5\xC5\xC8\xFD' for column 'sname' at
row 1
```

原因：服务器端认为你的客户端的字符集是utf-8，而实际上你的客户端的字符集是GBK。

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230115171232254.png)

查看所有字符集：`SHOW VARIABLES LIKE 'character_set_%';`

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230115171311405.png)

解决方案，设置当前连接的客户端字符集 “SET NAMES GBK;”

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230115171338546.png)

**问题5：修改数据库和表的字符编码**

修改编码：
（1)先停止服务，（2）修改my.ini文件（3）重新启动服务

说明：

如果是在修改my.ini之前建的库和表，那么库和表的编码还是原来的Latin1，要么删了重建，要么使用
alter语句修改编码。

```sql
mysql> create database 0728db charset Latin1;
Query OK, 1 row affected (0.00 sec)
```

```sql
mysql> use 0728db;
Database changed
```

```sql
mysql> create table student (id int , name varchar(20)) charset Latin1;
Query OK, 0 rows affected (0.02 sec)
mysql> show create table student\G
*************************** 1. row ***************************
Table: student
Create Table: CREATE TABLE `student` (
`id` int(11) NOT NULL,
`name` varchar(20) DEFAULT NULL,
PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1
1 row in set (0.00 sec)
```

```sql
mysql> alter table student charset utf8; #修改表字符编码为UTF8
Query OK, 0 rows affected (0.01 sec)
Records: 0 Duplicates: 0 Warnings: 0
mysql> show create table student\G
*************************** 1. row ***************************
Table: student
Create Table: CREATE TABLE `student` (
`id` int(11) NOT NULL,
`name` varchar(20) CHARACTER SET latin1 DEFAULT NULL, #字段仍然是latin1编码
PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8
1 row in set (0.00 sec)
mysql> alter table student modify name varchar(20) charset utf8; #修改字段字符编码为UTF8
Query OK, 0 rows affected (0.05 sec)
Records: 0 Duplicates: 0 Warnings: 0
mysql> show create table student\G
*************************** 1. row ***************************
Table: student
Create Table: CREATE TABLE `student` (
`id` int(11) NOT NULL,
`name` varchar(20) DEFAULT NULL,
PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8
1 row in set (0.00 sec)
```

```sql
mysql> show create database 0728db;;
+--------+-----------------------------------------------------------------+
|Database| Create Database |
+------+-------------------------------------------------------------------+
|0728db| CREATE DATABASE `0728db` /*!40100 DEFAULT CHARACTER SET latin1 */ |
+------+-------------------------------------------------------------------+
1 row in set (0.00 sec)
mysql> alter database 0728db charset utf8; #修改数据库的字符编码为utf8
Query OK, 1 row affected (0.00 sec)
mysql> show create database 0728db;
+--------+-----------------------------------------------------------------+
|Database| Create Database |
+--------+-----------------------------------------------------------------+
| 0728db | CREATE DATABASE `0728db` /*!40100 DEFAULT CHARACTER SET utf8 */ |
+--------+-----------------------------------------------------------------+
1 row in set (0.00 sec)
```

## 面试题

能够独立完成MySQL8.0、MySQL5.7版本的下载、安装、配置即可。



[返回首页](https://github.com/timerring/learn-MySQL)
