---
layout: post
title:  "不同数据库中SQL的不同"
excerpt: "修改TongWeb默认编码与TongWeb重启方法."
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
