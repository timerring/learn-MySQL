- [Basic chapter 1 - 数据库概述](#basic-chapter-1---数据库概述)
  - [数据库](#数据库)
  - [数据库与数据库管理系统](#数据库与数据库管理系统)
    - [数据库的相关概念](#数据库的相关概念)
      - [DB](#db)
      - [DBMS](#dbms)
      - [SQL](#sql)
    - [数据库与数据库管理系统的关系](#数据库与数据库管理系统的关系)
    - [常见的数据库管理系统排名(DBMS)](#常见的数据库管理系统排名dbms)
    - [常见的数据库简介](#常见的数据库简介)
      - [Oracle](#oracle)
      - [SQL Server](#sql-server)
      - [DB2](#db2)
      - [PostgreSQL](#postgresql)
      - [SQLite](#sqlite)
      - [informix](#informix)
  - [MySQL介绍](#mysql介绍)
    - [概述](#概述)
    - [发展历史图](#发展历史图)
  - [RDBMS与非RDBMS](#rdbms与非rdbms)
    - [关系型数据库(RDBMS)](#关系型数据库rdbms)
      - [优势](#优势)
    - [非关系型数据库(非RDBMS)](#非关系型数据库非rdbms)
      - [键值型数据库](#键值型数据库)
      - [文档型数据库](#文档型数据库)
      - [搜索引擎数据库](#搜索引擎数据库)
      - [列式数据库](#列式数据库)
      - [图形数据库](#图形数据库)
  - [关系型数据库设计规则](#关系型数据库设计规则)
    - [表、记录、字段](#表记录字段)
    - [表的关联关系](#表的关联关系)
      - [一对一关联（one-to-one）](#一对一关联one-to-one)
      - [一对多关系（one-to-many）](#一对多关系one-to-many)
      - [多对多（many-to-many）](#多对多many-to-many)
      - [自我引用(Self reference)](#自我引用self-reference)
  - [面试题](#面试题)


# Basic chapter 1 - 数据库概述

## 数据库

持久化(persistence)：把数据保存到可掉电式存储设备中以供之后使用。大多数情况下，特别是企业级应用，数据持久化意味着将内存中的数据保存到硬盘上加以”固化”，而持久化的实现过程大多通过各种关系数据库来完成。

持久化的主要作用是将**内存中的数据存储在关系型数据库中**，当然也可以存储在磁盘文件、XML数据文件中。

## 数据库与数据库管理系统

### 数据库的相关概念

#### DB

数据库（Database）

即存储数据的“仓库”，其本质是一个文件系统。它保存了一系列有组织的数据。

#### DBMS

数据库管理系统（Database Management System）

是一种操纵和管理数据库的大型软件，用于建立、使用和维护数据库，对数据库进行统一管理和控制。用户通过数据库管理系统访问数据库中表内的数据。

#### SQL

结构化查询语言（Structured Query Language）专门用来与数据库通信的语言。

### 数据库与数据库管理系统的关系

数据库管理系统(DBMS)可以管理多个数据库

+ 一般开发人员会针对每一个应用创建一个数据库。
+ 为保存应用中实体的数据，一般会在数据库创建多个表，以保存程序中实体用户的数据。

数据库管理系统、数据库和表的关系如图所示：

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230114151306036.png)

### 常见的数据库管理系统排名(DBMS)

2022年数据库的欢迎程度数据统计结果如下：（数据来源：https://db-engines.com/en/ranking）

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230114152212383.png)

相应的走势图如下：（数据来源：https://db-engines.com/en/ranking_trend）

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230114152311530.png)

### 常见的数据库简介

#### Oracle

商用（收费）数据库软件

#### SQL Server

SQL Server 是微软开发的大型商业数据库，诞生于 1989 年。C#、.net等语言常使用，与WinNT完全集成，也可以很好地与Microsoft BackOffice产品集成。

#### DB2

IBM公司的数据库产品, 收费。常应用在银行系统中。

#### PostgreSQL

PostgreSQL 的稳定性极强，最符合SQL标准，开放源码，具备商业级DBMS质量。PG对数据量大的文本以及SQL处理较快。

#### SQLite

**嵌入式的小型数据库**，应用在手机端。 零配置，SQlite3不用安装，不用配置，不用启动，关闭或者配置数据库实例。当系统崩溃后不用做任何恢复操作，再下次使用数据库的时候自动恢复。

#### informix

IBM公司出品，取自Information 和Unix的结合，它是**第一个被移植到Linux上的商业数据库产品**。仅运行于unix/linux平台，命令行操作。 性能较高，支持集群，适应于安全性要求极高的系统，尤其是银行，证券系统的应用。

## MySQL介绍

### 概述

MySQL是一个**开放源代码的关系型数据库管理系统**，由瑞典MySQL AB（创始人Michael Widenius）公司1995年开发。2008被Sun 收购，2009年Sun被Oracle 收购。MySQL 的创造者担心 MySQL 有闭源的风险，创建MySQL 的分支项目 MariaDB。

MySQL采用了`GPL（GNU General Public License）` 协议。

MySQL支持大型数据库，支持5000万条记录的数据仓库，32位系统表文件最大可支持4GB ，64位系统支持最大的表文件为8TB 。

MySQL可以允许运行于多个系统上，并且支持多种语言。这些编程语言包括C、C++、Python、Java、Perl、PHP和Ruby等。

### 发展历史图

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230114153456830.png)

MySQL从5.7版本直接跳跃发布了8.0版本，在功能上做了显著的改进与增强，开发者对MySQL的源代码进行了重构，最突出的一点是对MySQL Optimizer优化器进行了改进。

## RDBMS与非RDBMS

### 关系型数据库(RDBMS)

例如：`Oracle`、`MySQL` 和 `SQL Server`等等。

这种类型的数据库是最古老的数据库类型，关系型数据库模型是把复杂的数据结构归结为简单的`二元关系`（即二维表格形式）。

**关系型数据库以行(row) 和列(column) 的形式存储数据，以便于用户理解。这一系列的行和列被称为表(table) ，一组表组成了一个库(database)。**

表与表之间的数据记录有关系(relationship)。关系型数据库，就是建立在关系模型基础上的数据库。**SQL 就是关系型数据库的查询语言**。

#### 优势

**复杂查询**：可以用SQL语句方便的在一个表以及多个表之间做非常复杂的数据查询。

**事务支持**：使得对于安全性能很高的数据访问要求得以实现。

### 非关系型数据库(非RDBMS)

非关系型数据库，可看成传统关系型数据库的功能阉割版本，基于键值对存储数据，不需要经过SQL层的解析， 性能非常高。同时，通过减少不常用的功能，进一步提高性能。

#### 键值型数据库

键值型数据库通过 Key-Value 键值的方式来存储数据，其中 Key 和 Value 可以是简单的对象，也可以是复杂的对象。Key 作为唯一的标识符，优点是查找速度快，在这方面明显优于关系型数据库，缺点是无法像关系型数据库一样使用条件过滤（比如 WHERE），如果你不知道去哪里找数据，就要遍历所有的键，这就会消耗大量的计算。

**键值型数据库典型的使用场景是作为`内存缓存`。`Redis` 是最流行的键值型数据库。**

#### 文档型数据库

此类数据库可存放并获取文档，可以是XML、JSON等格式。在数据库中文档作为处理信息的基本单位，一个文档就相当于一条记录。文档数据库所存放的文档，就相当于键值数据库所存放的“值”。

MongoDB是最流行的文档型数据库。此外，还有CouchDB等。

#### 搜索引擎数据库

虽然关系型数据库采用了索引提升检索效率，但是针对全文索引效率却较低。搜索引擎数据库是应用在搜索引擎领域的数据存储形式，由于搜索引擎会爬取大量的数据，并以特定的格式进行存储，这样在检索的时候才能保证性能最优。核心原理是“倒排索引”。

典型产品：Solr、Elasticsearch、Splunk 等。

#### 列式数据库

列式数据库是相对于行式存储的数据库，Oracle、MySQL、SQL Server 等数据库都是采用的行式存储（Row-based），而列式数据库是将数据按照列存储到数据库中，这样做的好处是可以大量降低系统的I/O，适合于分布式文件系统，不足在于功能相对有限。

典型产品：HBase等。

#### 图形数据库

图形数据库，利用了图这种数据结构存储了实体（对象）之间的关系。图形数据库最典型的例子就是社交网络中人与人的关系，数据模型主要是以节点和边（关系）来实现，特点在于能高效地解决复杂的关系问题。

典型产品：Neo4J、InfoGrid等。

有些情况下，使用`性能更高`、`成本更低`的非关系型数据库是更明智的选择。比如：日志收集、排行榜、定时器等。

## 关系型数据库设计规则

关系型数据库的典型数据结构就是 `数据表` ，这些数据表的组成都是结构化的（Structured）。

一个数据库中可以有多个表，每个表都有一个名字，用来标识自己。表名具有唯一性。

### 表、记录、字段

E-R（entity-relationship，实体-联系）模型中有三个主要概念是： **实体集**、**属性**、**联系集**。

+ 一个实体集（class）对应于数据库中的一个表（table）
+ 一个实体（instance）则对应于数据库表中的一行（row），也称为一条记录（record）。
+ 一个属性（attribute）对应于数据库表中的一列（column），也称为一个字段（field）。

ORM思想 (Object Relational Mapping)体现

+ 数据库中的一个表 <---> Java或Python中的一个类
+ 表中的一条数据 <---> 类中的一个对象（或实体）
+ 表中的一个列 <----> 类中的一个字段、属性(field)

### 表的关联关系

表与表之间的数据记录有关系(relationship)。现实世界中的各种实体以及实体之间的各种联系均用关系模型来表示。

四种：一对一关联、一对多关联、多对多关联、自我引用

#### 一对一关联（one-to-one）

在实际的开发中应用不多，因为一对一可以创建成一张表。

两种建表原则：

+ 外键唯一：主表的主键和从表的外键（唯一），形成主外键关系，外键唯一。
+ 外键是主键：主表的主键和从表的主键，形成主外键关系。

#### 一对多关系（one-to-many）

一对多建表原则：在从表(多方)创建一个字段，字段作为外键指向主表(一方)的主键

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230114155835243.png)

#### 多对多（many-to-many）

要表示多对多关系，必须创建第三个表，该表通常称为`联接表`，它将多对多关系划分为两个一对多关系。将这两个表的主键都插入到第三个表中。

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230114155916878.png)

#### 自我引用(Self reference)

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230114160132538.png)

## 面试题

1.谈谈了解的常见的数据库

答：Oracle、MySQl、SQL Server、DB2、PGSQL；Redis、MongoDB、ES等等

2.谈谈你对MySQL历史、特点的理解

答：

+ 历史：
  + 由瑞典的MySQL AB 公司创立，1995开发出的MySQL
  + 2008年，MySQL被SUN公司收购
  + 2009年，Oracle收购SUN公司，进而Oracle就获取了MySQL
  + 2016年，MySQL8.0.0版本推出
+ 特点：
  + 开源的、关系型的数据库
  + 支持千万级别数据量的存储，大型的数据库

3.说说你对DB、DBMS、SQL的理解

答：

+ DB：database，看做是数据库文件。
+ DBMS：数据库管理系统。

**MySQL数据库服务器中安装了MySQL DBMS, 使用MySQL DBMS 来管理和操作DB，使用的是SQL语言。**

4.你知道哪些非关系型数据库？

+ 键值型数据库：Redis
+ 文档型数据库：MongoDB
+ 搜索引擎数据库：ES、Solr
+ 列式数据库：HBase
+ 图形数据库：InfoGrid

5.表与表的记录之间存在哪些关联关系？

+ ORM思想：Object-Relational Mapping，它的作用是在关系型数据库和对象之间作一个映射，这样，我们在具体的操作数据库的时候，就不需要再去和复杂的SQL语句打交道，只要像平时操作对象一样操作它就可以了。表，数据，字段。
+ 表与表的记录之间的关系：一对一关系、一对多关系、多对多关系、自关联。



[返回首页](https://github.com/timerring/learn-MySQL)