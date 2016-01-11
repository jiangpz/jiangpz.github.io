---
layout: post
title:  "不同数据库中SQL的不同"
excerpt: "不同数据库中SQL函数存在不同."
date:   2015-12-30 15:46:21 +0800
categories: SQL
tags: [SQl, Oracle，MySQL]
---

在编写完SQL后需要在不同的数据库中运行，不同的数据的SQL函数和语法还算有些区别的，在读《SQL Cookbook》的同时，将这些区别记录下来。建库脚本在[这里](http://examples.oreilly.com/9780596009762/sql_cookbook.zip)。

### 检索记录

##### 连接列值

 - Oracle，DB2，PostgreSQL

    这些数据库使用双竖线作为连接运算符。

    {% highlight sql linenos %}
    select ename||' WORK AS A '||job as msg
      from emp
     where deptno=10
    {% endhighlight %}

 - MySQL

    这个数据库支持CONCAT函数。

    {% highlight sql linenos %}
    select concat(ename, ' WORK AS A ', job) as msg
      from emp
     where deptno=10
    {% endhighlight %}


 - SQL Server

    使用“+”运算符进行连接操作。

    {% highlight sql linenos %}
    select ename + ' WORK AS A ' + job as msg
      from emp
     where deptno=10
    {% endhighlight %}

##### 限制返回的行数

- DB2

   使用FETCH FIRST子句。

   {% highlight sql linenos %}
   select *
     from emp fetch first 5 rows only
   {% endhighlight %}

 - Oracle

    在WHERE子句中通过使用ROWNUM来限制行数。

    {% highlight sql linenos %}
    select *
      from emp
     where rownum <= 5
    {% endhighlight %}

 - MySQL, PostgreSQL

    使用LIMIT。

    {% highlight sql linenos %}
    select *
      from emp limit 5
    {% endhighlight %}


 - SQL Server

    使用TOP关键字，来限制返回的行数。

    {% highlight sql linenos %}
    select top 5 *
      from emp
    {% endhighlight %}

##### 从表中随机返回n条记录

- DB2

   使用内置函数RAND与ORDER BY和FETCH FIRST。

   {% highlight sql linenos %}
   select ename,job
     from emp
    order by rahnd() fetch first 5 rows only
   {% endhighlight %}

 - Oracle

    同时使用DBMS_RANDOM包中的内置函数VALUE、ORDER BY和内置函数ROWNUM来限制行数。

    {% highlight sql linenos %}
    select *
      from (
    select ename, job
      from emp
      order by dbms_random.value()
            )
     where rownum <= 5
    {% endhighlight %}

 - MySQL

    使用内置的RAND函数、LIMIT和ORDER BY。

    {% highlight sql linenos %}
    select ename,job
      from emp
     order by rand() limit 5
    {% endhighlight %}

 - PostgreSQL

    使用内置的RANDOM函数、LIMIT和ORDER BY。

    {% highlight sql linenos %}
    select ename,job
      from emp
     order by random() limit 5
    {% endhighlight %}

 - SQL Server

    同时使用内置函数NEWID、TOP和ORDER BY。

    {% highlight sql linenos %}
    select top 5 ename, job
      from emp
     order by newid()
    {% endhighlight %}

### 查询结果排序

##### 按子串排序

- DB2、MySQL、Oracle和PostgreSQL

   在ORDER BY 子句中使用SUBSTR函数。

   {% highlight sql linenos %}
   select ename,job
     from emp
    order by substr(job,length(job)-2)
   {% endhighlight %}

 - SQL Server

    在ORDER BY 子句中使用SUBSTRING函数。

    {% highlight sql linenos %}
    select ename,job
      from emp
     order by substring(job,length(job)-2,2)
    {% endhighlight %}

##### 字符串与字符替换

- Oracle、PostgreSQL

   使用函数REPLACE和TRANSLATE修改要排序的字符串

 - DB2

    DB2中隐式转换比在Oracle或PostgreSQL中更为严格。需要将待处理文本转换为CHAR类型。

 - SQL Server、MySQL

    不支持TRANSLATE函数

##### 处理排序空值

在EMP中根据COMM排序，这个字段可以有空值，需要指定是否将空值排在最后。

- PostgreSQL、DB2、SQL Server、MySQL

    使用CASE

 - Oracle

    可使用与其他平台相同解决方案，但是Oracle 9i后可以子啊ORDER BY中使用NULLS FIRST或NULLS LAST，更简洁。

### 操作多个表

##### 在两个表中找供同行

 - MySQL、SQL Server

    使用多个连接条件

 - DB2、Oracle和PostgreSQL

    使用INTERSECT以及IN

##### 从一个表中查找另外一个表没有的值

 - DB2和PostgreSQL

    使用集合操作EXCEPT。

    {% highlight sql linenos %}
    select deptno from dept
    except
    select deptno from emp
    {% endhighlight %}

 - Oracle

    使用集合操作MINUS。

    {% highlight sql linenos %}
    select deptno from dept
    minus
    select deptno from emp
    {% endhighlight %}  

 - MySQL和SQL Server

    使用子查询返回表EMP中所有的DEPTNO，而外层查询则从DEPT表中查找子查询的结果中没有的行。

    {% highlight sql linenos %}
    select deptno
      from dept
     where deptno not in (select deptno from emp)
    {% endhighlight %}

##### 从一个表中查找与其他表不匹配的记录

 - DB2、PostgreSQL、MySQL和SQL Server

    使用外联接及NULL筛选(OUTER关键字是可选的)。

    {% highlight sql linenos %}
    select d.*
      from dept d left outer join emp e
     where e.deptno is null
    {% endhighlight %}

 - Oracle

    在Oracle9i之前可使用上面的解决方案，也可使用Oracle特有的外联接语法。

    {% highlight sql linenos %}
    select d.*
      from dept d, emp e
     where d.deptno = d.deptno (+)
       and e.deptno is null
    {% endhighlight %}  

### 插入、更新与删除

##### 复制表定义

要创建新表，该表与已有表的列设置相同，但只是想复制表结构而不想复制源表中的记录。

- DB2

   使用带有LIKE子句的CREATE TABLE命令。

   {% highlight sql linenos %}
   creat table dept_2 like dept
   {% endhighlight %}

- MySQL、Oracle和PostgreSQL

   在CREATE TABLE命令中，使用一个不返回任何行的子查询。

   {% highlight sql linenos %}
   create table dept_2
   as
   select *
     from dept
    where 1= 0
   {% endhighlight %}

 - SQL Server

    使用带有不返回任何行的查询和INTO子句。

    {% highlight sql linenos %}
    select *
      into dept_2
      from dept
     where 1 = 0
    {% endhighlight %}

##### 一次向多个表中插入记录

要创建新表，该表与已有表的列设置相同，但只是想复制表结构而不想复制源表中的记录。

- Oracle

   使用INSERT ALL或INSERT FIRST语句。这两种方法除了关键字ALL与FIRST不同外，其语法都相同。下面的语句使用了INSERT ALL命令来同时兼顾所有的目标表：

   {% highlight sql linenos %}
   insert all
     when loc in ('NEW YORK', 'BOSTON') then
       into dept_east (deptno,dname,loc) values (deptno,dname,loc)
     when loc = 'CHICAGO' then
       into dept_mid  (deptno,dname,loc) values (deptno,dname,loc)
     else
       into dept_west (deptno,dname,loc) values (deptno,dname,loc)
   select deptno,dname,loc
     from dept
   {% endhighlight %}

- DB2

   将所有目标表用UNION ALL构成一个内联视图，并以内联视图作为INSERT INTO的目标。必须要在这些表中设置约束条件，以确保这些行插入到正确的表中。

   {% highlight sql linenos %}
   creat table dept_east
   ( deptno integer,
     dname  varchar(10),
     loc    varchar(10) check (loc in ('NEW YORK', 'BOSTON')))

   creat table dept_mid
   ( deptno integer,
     dname  varchar(10),
     loc    varchar(10) check (loc in ('CHICAGO')))

   creat table dept_west
   ( deptno integer,
     dname  varchar(10),
     loc    varchar(10) check (loc in ('DALLAS')))

   insert into (
     select * from dept_west union all
     select * from dept_east union all
     select * from dept_mid
   ) select * from dept
   {% endhighlight %}

- MySQL、SQL Server和PostgreSQL

   暂不支持。

##### 合并记录

要创建新表，该表与已有表的列设置相同，但只是想复制表结构而不想复制源表中的记录。

- Oracle

  是目前唯一具有可以解决此问题的RDBMS。该语句为MERGE，它能够按需要执行UPDATE或INSERT操作，例如：

  {% highlight sql linenos %}
  merge into emp_commission ec
  using (select I from emp) emp
     on (ec.empno=emp.empno)
   when matched then
        update set ec.comm = 1000
        delete where (sal < 2000)
   when not matched then
        insert (ec.empno,ec.ename,ec,deptno,ec.comm)
        values (emp.empno,emp.ename,emp,deptno,emp.comm)
  {% endhighlight %}

### 元数据查询

##### 列出模式中的表

查看在给出的模式中所有已创建的表的清单。通过查询一个包含着数据库中所有表名称的系统（或试图）实现。

- DB2

   查询SYSCAT.TABLES：

   {% highlight sql linenos %}
   select tabname
     from syscat.TABLES
    where tabschema = 'SMEAGOL'
   {% endhighlight %}   

 - Oracle

    查询SYS.ALL_TABLES：

    {% highlight sql linenos %}
    select table_name
      from all_tables
     where owner = 'SMEAGOL'
    {% endhighlight %}

 - PostgreSQL、MySQL和SQL Server

    查询INFORMATION_SCHEMA.TABLES：

    {% highlight sql linenos %}
    select table_name
      from information_schema.tables
     where table_schema = 'SMEAGOL'
    {% endhighlight %}

##### 列出表的列

列出表的各列、他们的数据类型，以及这些列在表中的位置。

- DB2

   查询SYSCAT.COLUMNS：

   {% highlight sql linenos %}
   select colname, typename, colno
     from syscat.columns
    where tabname   = 'EMP'
      and tabschema = 'SMEAGOL'
   {% endhighlight %}   

 - Oracle

    查询ALL_TAB_COLUMNS：

    {% highlight sql linenos %}
    select column_name, data_type, columm_id
      from all_tab_columns
     where owner      = 'SMEAGOL'
       and table_name = 'EMP'
    {% endhighlight %}

 - PostgreSQL、MySQL和SQL Server

    查询INFORMATION_SCHEMA.COLUMNS：

    {% highlight sql linenos %}
    select column_name, data_type, ordinal_position
      from information_schema.columns
     where table_schema = 'SMEAGOL'
       and table_name   = 'EMP'
    {% endhighlight %}

##### 列出表的索引列

- DB2

   查询SYSCAT.INDEXES

 - Oracle

    查询SYS.ALL_IND_COLUMNS

 - PostgreSQL

    查询PG_CATALOG.PG_INDEXES和INFORMATION_SCHEMA.COLUMNS

 - MySQL

    使用SHOW INDEX命令

 - SQL Server

    查询SYS.TABLES、SYS.INDEXES、SYS.INDEX_COLUMNS和SYS.COLUMNS

##### 列出表的约束

- DB2

   查询SYSCAT.TABCONST和SYSCAT.COLUMNS

 - Oracle

    查询SYS.ALL_CONSTRAINTS和SYS.ALL_CONS_COLUMNS

 - PostgreSQL、MySQL和SQL Server

    查询INFORMATION_SCHEMA.TABLE_CONSTRAINTS和INFORMATION_SCHEMA.KEY_COLUMN_USAGE

##### 列出没有相应索引的外键

- DB2

   查询SYSCAT.TABCONST、SYSCAT.KEYCOLUSE、SYSCAT.INDEXES和SYSCAT.INDEXCOLUSE

 - Oracle

    查询SYS.ALL_CONSTRAINTS、SYS.ALL_IND_COLUMNS和SYS.ALL_CONS_COLUMNS

 - PostgreSQL

    使用SHOW INDEX命令来检索索引信息

 - MySQL

    查询INFORMATION_SCHEMA.TABLE_CONSTRAINTS和INFORMATION_SCHEMA.KEY_COLUMN_USAGE

 - SQL Server

    查询SYS_TABLES、SYS.FOREIGN_KEYS、SYS.COLUMNS、SYS.INDEXES和SYS.INDEX_COLUMNS

### 使用字符串

##### 按字符串中的部分内容排序

- DB2、Oracle、MySQL和PostgreSQL

   联合使用内置函数LENGTH和SUBSTR来按照字符串的指定部分进行排序：

   {% highlight sql linenos %}
   select ename
     from emp
    order by substr(ename,length(ename)-1,2)
   {% endhighlight %}   

 - SQL Server

    使用SUBSTRING和LEN来按照字符串的指定部分进行排序：

    {% highlight sql linenos %}
    select ename
      from emp
     order by substring(ename,len(ename)-1,2)
    {% endhighlight %}

### 使用数字

##### 计算中间值

- DB2

   使用窗口函数COUNT(\*)  OVER 和 ROW_NUMBER，查找中间数

- MySQL和PostgreSQL

   使用自连接查找中间数   

- Oracle

   使用函数MEDIAN(Oracle Database 10h)或PERCENTITLE_COUNT(Oracle9i)   

 - SQL Server

    使用窗口函数COUNT(\*)  OVER 和 ROW_NUMBER，查找中间数

##### 计算不包含最大值和最小值的均值

- MySQL和PostgreSQL

   使用子查询排除最高和最低值：

   {% highlight sql linenos %}
   select avg(sal)
     from emp
   where sal not in (
     (select min(sal) from emp),
     (select max(sal) from emp)
     )
   {% endhighlight %}   

 - DB2、Oracle、SQL Server

    使用内联视图及窗口函数MAX OVER和MIN OVER， 生成一个结果集，可以很容易地从中剔除最大和最小值：

    {% highlight sql linenos %}
    select avg(sal)
      from (
           select sal,min(sal) over() min_sal, max(sal) over() max_sal
             from emp
           ) x
     where sal not in (min_sal,max_sal)
    {% endhighlight %}
