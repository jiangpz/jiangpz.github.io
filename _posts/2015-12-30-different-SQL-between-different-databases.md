---
layout: post
title:  "不同数据库中SQL的不同"
excerpt: "不同数据库中SQL函数存在不同."
date:   2015-12-30 15:46:21 +0800
categories: SQL
tags: [SQl, Oracle，MySQL]
comments: true
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

### 日期运算

使用同一种日期格式，即“DD-MON-YYYY”。

##### 加减日/月/年

- DB2

  {% highlight sql linenos %}
  select hiredate -5 day   as hd_minus_5D,
         hiredate +5 day   as hd_plus_5D,
         hiredate -5 month as hd_minus_5M,
         hiredate +5 month as hd_plus_5M,
         hiredate -5 year  as hd_minus_5Y,
         hiredate +5 year  as hd_plus_5Y
    from emp
   where deptno = 10
  {% endhighlight %}

- Oracle

  {% highlight sql linenos %}
  select hiredate-5 as hd_minus_5D,
         hiredate+5 as hd_plus_5D,
         add_months(hiredate,-5) as hd_minus_5M,
         add_months(hiredate,5)  as hd_plus_5M,
         add_months(hiredate,-5*12) as hd_minus_5Y,
         add_months(hiredate,5*12) as hd_plus_5Y
    from emp
   where deptno = 10
  {% endhighlight %}

- PostgreSQL

  {% highlight sql linenos %}
  select hiredate - interval '5 day'   as hd_minus_5D,
        hiredate + interval '5 day'   as hd_plus_5D,
        hiredate - interval '5 month' as hd_minus_5M,
        hiredate + interval '5 month' as hd_plus_5M,
        hiredate - interval '5 year'  as hd_minus_5Y,
        hiredate + interval '5 year'  as hd_plus_5Y
        from emp
        where deptno=10
  {% endhighlight %}   

- MySQL

  {% highlight sql linenos %}
  select hiredate - interval 5 day   as hd_minus_5D,
         hiredate + interval 5 day   as hd_plus_5D,
         hiredate - interval 5 month as hd_minus_5M,
         hiredate + interval 5 month as hd_plus_5M,
         hiredate - interval 5 year  as hd_minus_5Y,
         hiredate + interval 5 year  as hd_plus_5Y
    from emp
   where deptno=10
  {% endhighlight %}   

  或者

  {% highlight sql linenos %}
  select date_add(hiredate,interval -5 day)   as hd_minus_5D,
         date_add(hiredate,interval  5 day)   as hd_plus_5D,
         date_add(hiredate,interval -5 month) as hd_minus_5M,
         date_add(hiredate,interval  5 month) as hd_plus_5M,
         date_add(hiredate,interval -5 year)  as hd_minus_5Y,
         date_add(hiredate,interval  5 year)  as hd_plus_5DY
    from emp
   where deptno=10
  {% endhighlight %}   

 - SQL Server

  {% highlight sql linenos %}
  select dateadd(day,-5,hiredate)   as hd_minus_5D,
        dateadd(day,5,hiredate)    as hd_plus_5D,
        dateadd(month,-5,hiredate) as hd_minus_5M,
        dateadd(month,5,hiredate)  as hd_plus_5M,
        dateadd(year,-5,hiredate)  as hd_minus_5Y,
        dateadd(year,5,hiredate)   as hd_plus_5Y
   from emp
  where deptno = 10
  {% endhighlight %}

##### 计算两个日期之间的天数

- DB2

  {% highlight sql linenos %}
  select days(ward_hd) - days(allen_hd)
    from (
  select hiredate as ward_hd
    from emp
   where ename = 'WARD'
         ) x,
         (
  select hiredate as allen_hd
    from emp
   where ename = 'ALLEN'
         ) y
  {% endhighlight %}

- Oracle 和 PostgreSQL

  {% highlight sql linenos %}
  select ward_hd - allen_hd
    from (
  select hiredate as ward_hd
    from emp
   where ename = 'WARD'
         ) x,
         (
  select hiredate as allen_hd
    from emp
   where ename = 'ALLEN'
         ) y
  {% endhighlight %}

- MySQL 和 SQL Server

  {% highlight sql linenos %}
  select datediff(day,allen_hd,ward_hd)
    from (
  select hiredate as ward_hd
    from emp
   where ename = 'WARD'
         ) x,
         (
  select hiredate as allen_hd
    from emp
   where ename = 'ALLEN'
         ) y
  {% endhighlight %}

##### 确定两个日期之间的工作日数目

首先计算起始日期和结束日期之间的天数，再计算除周末外共有多少天（即行数）

- DB2

  {% highlight sql linenos %}
  select sum(case when dayname(jones_hd+t500.id day -1 day)
                    in ( 'Saturday','Sunday' )
                  then 0 else 1
             end) as days
    from (
  select max(case when ename = 'BLAKE'
                  then hiredate
             end) as blake_hd,
         max(case when ename = 'JONES'
                  then hiredate
             end) as jones_hd
    from emp
   where ename in ( 'BLAKE','JONES' )
         ) x,
         t500
   where t500.id <= blake_hd-jones_hd+1
  {% endhighlight %}

- MySQL

  {% highlight sql linenos %}
  select sum(case when date_format(
                          date_add(jones_hd,
                                   interval t500.id-1 DAY),'%a')
                    in ( 'Sat','Sun' )
                  then 0 else 1
             end) as days
    from (
  select max(case when ename = 'BLAKE'
                  then hiredate
             end) as blake_hd,
         max(case when ename = 'JONES'
                  then hiredate
              end) as jones_hd
    from emp
   where ename in ( 'BLAKE','JONES' )
         ) x,
         t500
   where t500.id <= datediff(blake_hd,jones_hd)+1
  {% endhighlight %}

- PostgreSQL

  {% highlight sql linenos %}
  select sum(case when trim(to_char(jones_hd+t500.id-1,'DAY'))
                    in ( 'SATURDAY','SUNDAY' )
                  then 0 else 1
             end) as days
    from (
  select max(case when ename = 'BLAKE'
                  then hiredate
             end) as blake_hd,
         max(case when ename = 'JONES'
                  then hiredate
             end) as jones_hd
    from emp
   where ename in ( 'BLAKE','JONES' )
         ) x,
         t500
   where t500.id <= blake_hd-jones_hd+1
  {% endhighlight %}

- SQL Server

  {% highlight sql linenos %}
  select sum(case when datename(dw,jones_hd+t500.id-1)
                    in ( 'SATURDAY','SUNDAY' )
                   then 0 else 1
             end) as days
    from (
  select max(case when ename = 'BLAKE'
                  then hiredate
             end) as blake_hd,
         max(case when ename = 'JONES'
                  then hiredate
             end) as jones_hd
    from emp
   where ename in ( 'BLAKE','JONES' )
         ) x,
         t500
   where t500.id <= datediff(day,jones_hd-blake_hd)+1
  {% endhighlight %}

#### 确定两个日期之间的月份数或年数

- DB2 and MySQL

  {% highlight sql linenos %}
  select mnth, mnth/12
    from (
  select (year(max_hd) - year(min_hd))*12 +
         (month(max_hd) - month(min_hd)) as mnth
    from (
  select min(hiredate) as min_hd, max(hiredate) as max_hd
    from emp
         ) x
         ) y
  {% endhighlight %}

- Oracle

  {% highlight sql linenos %}
  select months_between(max_hd,min_hd),
         months_between(max_hd,min_hd)/12
    from (
  select min(hiredate) min_hd, max(hiredate) max_hd
    from emp
         ) x
  {% endhighlight %}

- PostgreSQL

{% highlight sql linenos %}
select mnth, mnth/12
  from (
select ( extract(year from max_hd)
         extract(year from min_hd) ) * 12
       +
       ( extract(month from max_hd)
         extract(month from min_hd) ) as mnth
  from (
select min(hiredate) as min_hd, max(hiredate) as max_hd
  from emp
       ) x
       ) y
{% endhighlight %}

- SQL Server

  {% highlight sql linenos %}
  select datediff(month,min_hd,max_hd),
         datediff(month,min_hd,max_hd)/12
    from (
  select min(hiredate) min_hd, max(hiredate) max_hd
    from emp
         ) x
  {% endhighlight %}

#### 确定两个日期之间的秒、分、小时数

知道了两个日期之间的天数，就可以计算出秒、分、小时数。

- DB2

  {% highlight sql linenos %}
  select dy*24 hr, dy*24*60 min, dy*24*60*60 sec
    from (
  select ( days(max(case when ename = 'WARD'
                    then hiredate
               end)) -
           days(max(case when ename = 'ALLEN'
                    then hiredate
               end))
         ) as dy
    from emp
         ) x
  {% endhighlight %}

- MySQL and SQL Server

  {% highlight sql linenos %}
  select datediff(day,allen_hd,ward_hd)*24 hr,
         datediff(day,allen_hd,ward_hd)*24*60 min,
         datediff(day,allen_hd,ward_hd)*24*60*60 sec
    from (
  select max(case when ename = 'WARD'
                   then hiredate
             end) as ward_hd,
         max(case when ename = 'ALLEN'
                  then hiredate
             end) as allen_hd
    from emp
         ) x
  {% endhighlight %}

- Oracle and PostgreSQL

  {% highlight sql linenos %}
  select dy*24 as hr, dy*24*60 as min, dy*24*60*60 as sec
    from (
  select (max(case when ename = 'WARD'
                  then hiredate
             end) -
         max(case when ename = 'ALLEN'
                  then hiredate
             end)) as dy
    from emp
        ) x
  {% endhighlight %}

#### 确定当前记录和下一条记录之间相差的天数

- DB2

  {% highlight sql linenos %}
  select x.*,
         days(x.next_hd) - days(x.hiredate) diff
    from (
  select e.deptno, e.ename, e.hiredate,
         (select min(d.hiredate) from emp d
           where d.hiredate > e.hiredate) next_hd
    from emp e
   where e.deptno = 10
         ) x
  {% endhighlight %}

- MySQL and SQL Server

  {% highlight sql linenos %}
  select x.*,
         datediff(day,x.hiredate,x.next_hd) diff
    from (
  select e.deptno, e.ename, e.hiredate,
         (select min(d.hiredate) from emp d
           where d.hiredate > e.hiredate) next_hd
    from emp e
   where e.deptno = 10
         ) x
  {% endhighlight %}

- Oracle

使用LEAD OVER：

  {% highlight sql linenos %}
  select ename, hiredate, next_hd,
         next_hd - hiredate diff
    from (
  select deptno, ename, hiredate,
         lead(hiredate)over(order by hiredate) next_hd
    from emp
         )
   where deptno=10
  {% endhighlight %}

- PostgreSQL

  {% highlight sql linenos %}
  select x.*,
         x.next_hd - x.hiredate as diff
    from (
  select e.deptno, e.ename, e.hiredate,
         (select min(d.hiredate) from emp d
           where d.hiredate > e.hiredate) as next_hd
    from emp e
   where e.deptno = 10
         ) x
  {% endhighlight %}

### 日期操作

使用同一种日期格式，即“DD-MON-YYYY”。

##### 确定一年是否为闰年

检查2月的最后一天，如果它为29，则当前年为闰年。

- DB2

  {% highlight sql linenos %}
    with x (dy,mth)
      as (
  select dy, month(dy)
    from (
  select (current_date -
           dayofyear(current_date) days +1 days)
            +1 months as dy
    from t1
         ) tmp1
   union all
  select dy+1 days, mth
    from x
   where month(dy+1 day) = mth
  )
  select max(day(dy))
    from x
  {% endhighlight %}

- Oracle

  {% highlight sql linenos %}
  select to_char(
           last_day(add_months(trunc(sysdate,'y'),1)),
          'DD')
    from t1
  {% endhighlight %}

- PostgreSQL

  {% highlight sql linenos %}
  select max(to_char(tmp2.dy+x.id,'DD')) as dy
    from (
  select dy, to_char(dy,'MM') as mth
    from (
  select cast(cast(
              date_trunc('year',current_date) as date)
                         + interval '1 month' as date) as dy
    from t1
         ) tmp1
         ) tmp2, generate_series (0,29) x(id)
   where to_char(tmp2.dy+x.id,'MM') = tmp2.mth
  {% endhighlight %}

- MySQL

  {% highlight sql linenos %}
  select day(
         last_day(
         date_add(
         date_add(
         date_add(current_date,
                  interval -dayofyear(current_date) day),
                  interval 1 day),
                  interval 1 month))) dy
    from t1
  {% endhighlight %}

- SQL Server

  {% highlight sql linenos %}
    with x (dy,mth)
      as (
  select dy, month(dy)
    from (
  select dateadd(mm,1,(getdate( )-datepart(dy,getdate( )))+1) dy
    from t1
         ) tmp1
   union all
  select dateadd(dd,1,dy), mth
    from x
   where month(dateadd(dd,1,dy)) = mth
  )
  select max(day(dy))
    from x
  {% endhighlight %}

#### 确定一年的天数

首先找到当前年的第一天，接着给该日期加1年，最后从上一步的结果中减去当前年。

- DB2

  {% highlight sql linenos %}
  select days((curr_year + 1 year)) - days(curr_year)
    from (
  select (current_date -
          dayofyear(current_date) day +
           1 day) curr_year
    from t1
         ) x
  {% endhighlight %}

- Oracle

  {% highlight sql linenos %}
  select add_months(trunc(sysdate,'y'),12) - trunc(sysdate,'y')
	  from dual
  {% endhighlight %}

- PostgreSQL

  {% highlight sql linenos %}
  select cast((curr_year + interval '1 year') as date) - curr_year
	  from (
	select cast(date_trunc('year',current_date) as date) as curr_year
	  from t1
	       ) x
  {% endhighlight %}

- MySQL

  {% highlight sql linenos %}
  select datediff((curr_year + interval 1 year),curr_year)
	  from (
	select adddate(current_date,-dayofyear(current_date)+1) curr_year
	  from t1
	       ) x
  {% endhighlight %}

- SQL Server

  {% highlight sql linenos %}
  select datediff(d,curr_year,dateadd(yy,1,curr_year))
	  from (
	select dateadd(d,-datepart(dy,getdate())+1,getdate()) curr_year
	  from t1
	       ) x
  {% endhighlight %}

#### 从日期中提取时间的各部分

- DB2

  {% highlight sql linenos %}
  select    hour( current_timestamp ) hr,
	        minute( current_timestamp ) min,
	        second( current_timestamp ) sec,
	           day( current_timestamp ) dy,
	         month( current_timestamp ) mth,
	           year( current_timestamp ) yr
	  from t1
  {% endhighlight %}

- Oracle

  {% highlight sql linenos %}
   select to_number(to_char(sysdate,'hh24')) hour,
          to_number(to_char(sysdate,'mi')) min,
          to_number(to_char(sysdate,'ss')) sec,
          to_number(to_char(sysdate,'dd')) day,
          to_number(to_char(sysdate,'mm')) mth,
          to_number(to_char(sysdate,'yyyy')) year
    from dual
  {% endhighlight %}

- PostgreSQL

  {% highlight sql linenos %}
  select to_number(to_char(current_timestamp,'hh24'),'99') as hr,
	       to_number(to_char(current_timestamp,'mi'),'99') as min,
	       to_number(to_char(current_timestamp,'ss'),'99') as sec,
	       to_number(to_char(current_timestamp,'dd'),'99') as day,
	       to_number(to_char(current_timestamp,'mm'),'99') as mth,
	       to_number(to_char(current_timestamp,'yyyy'),'9999') as yr
	  from t1
  {% endhighlight %}

- MySQL

  {% highlight sql linenos %}
  select date_format(current_timestamp,'%k') hr,
	       date_format(current_timestamp,'%i') min,
	       date_format(current_timestamp,'%s') sec,
	       date_format(current_timestamp,'%d') dy,
	       date_format(current_timestamp,'%m') mon,
	       date_format(current_timestamp,'%Y') yr
	  from t1
  {% endhighlight %}

- SQL Server

  {% highlight sql linenos %}
  select datepart( hour, getdate()) hr,
	       datepart( minute,getdate()) min,
	       datepart( second,getdate()) sec,
	       datepart( day, getdate()) dy,
	       datepart( month, getdate()) mon,
	       datepart( year, getdate()) yr
	  from t1
  {% endhighlight %}

#### 确定某个月的第一天和最后一天

- DB2

  {% highlight sql linenos %}
  select (current_date - day(current_date) day +1 day) firstday,
	       (current_date +1 month -day(current_date) day) lastday
	  from t1
  {% endhighlight %}

- Oracle

  {% highlight sql linenos %}
  select trunc(sysdate,'mm') firstday,
	       last_day(sysdate) lastday
	  from dual
  {% endhighlight %}

- PostgreSQL

  {% highlight sql linenos %}
  select firstday,
	       cast(firstday + interval '1 month'
	                     - interval '1 day' as date) as lastday
	  from (
	select cast(date_trunc('month',current_date) as date) as firstday
	  from t1
	       ) x
  {% endhighlight %}

- MySQL

  {% highlight sql linenos %}
  select date_add(current_date,
	                interval -day(current_date)+1 day) firstday,
	       last_day(current_date) lastday
	  from t1
  {% endhighlight %}

- SQL Server

  {% highlight sql linenos %}
  select dateadd(day,-day(getdate( ))+1,getdate( )) firstday,
	       dateadd(day,
	               -day(getdate( )),
	               dateadd(month,1,getdate( ))) lastday
	  from t1
  {% endhighlight %}

### 高级查找

#### 给结果集分页

- DB2、Oracle和SQL Server

  {% highlight sql linenos %}
  select sal
    from (
  select row_number( ) over (order by sal) as rn,
         sal
    from emp
         ) x
   where rn between 1 and 5
  {% endhighlight %}

- MySQL和PostgreSQL

  {% highlight sql linenos %}
  select sal
	  from emp
	 order by sal limit 5 offset 0
  {% endhighlight %}

#### 跳过表中n行

- DB2、Oracle和SQL Server

  {% highlight sql linenos %}
  select ename
    from (
  select row_number( ) over (order by ename) rn,
         ename
    from emp
         ) x
   where mod(rn,2) = 1
  {% endhighlight %}

- MySQL和PostgreSQL

  {% highlight sql linenos %}
  select x.ename
    from (
  select a.ename,
    (select count(*)
            from emp b
            where b.ename <= a.ename) as rn
     from emp a
          ) x
   where mod(x.rn,2) = 1
  {% endhighlight %}

#### 在外联接中用OR逻辑

- DB2, MySQL, PostgreSQL, and SQL Server

  {% highlight sql linenos %}
  select e.ename, d.deptno, d.dname, d.loc
    from dept d left join emp e
      on (d.deptno = e.deptno
         and (e.deptno=10 or e.deptno=20))
   order by 2
  {% endhighlight %}

  或者

  {% highlight sql linenos %}
  select e.ename, d.deptno, d.dname, d.loc
    from dept d
    left join
         (select ename, deptno
            from emp
           where deptno in ( 10, 20 )
         ) e on ( e.deptno = d.deptno )
  order by 2
  {% endhighlight %}

-  Oracle

  Oracle9i和之后的产品可使用上面的方案

#### 找到包含最大值和最小值的记录

- DB2, Oracle, and SQL Server

  {% highlight sql linenos %}
  select ename
    from (
  select ename, sal,
         min(sal)over( ) min_sal,
         max(sal)over( ) max_sal
    from emp
         ) x
   where sal in (min_sal,max_sal)
  {% endhighlight %}

- MySQL and PostgreSQL

  {% highlight sql linenos %}
  select ename
    from emp
   where sal in ( (select min(sal) from emp),
                  (select max(sal) from emp) )
  {% endhighlight %}

#### 存取“未来”行

  找到满足这样条件的员工：即他的收入紧随其后聘用的员工要少

- DB2, MySQL, PostgreSQL, and SQL Server

  {% highlight sql linenos %}
  select ename, sal, hiredate
    from (
  select a.ename, a.sal, a.hiredate,
        (select min(hiredate) from emp b
          where b.hiredate > a.hiredate
            and b.sal > a.sal ) as next_sal_grtr,
        (select min(hiredate) from emp b
          where b.hiredate > a.hiredate) as next_hire
    from emp a
         ) x
    where next_sal_grtr = next_hire
  {% endhighlight %}

- Oracle

  {% highlight sql linenos %}
  select ename, sal, hiredate
    from (
  select ename, sal, hiredate,
         lead(sal)over(order by hiredate) next_sal
    from emp
         )
   where sal < next_sal
  {% endhighlight %}

### 报表和数据仓库运算

#### 将结果转置为一行

  将：

  {% highlight text %}
  DEPTNO        CNT
------ ----------
    10          3
    20          5
    30          6
  {% endhighlight %}

  转换为：

  {% highlight text %}
  DEPTNO_10   DEPTNO_20   DEPTNO_30
---------  ----------  ----------
        3           5           6
  {% endhighlight %}

- ALL

{% highlight sql linenos %}
select sum(case when deptno=10 then 1 else 0 end) as deptno_10,
       sum(case when deptno=20 then 1 else 0 end) as deptno_20,
       sum(case when deptno=30 then 1 else 0 end) as deptno_30
  from emp
{% endhighlight %}

#### 创建横向直方图

例如：

{% highlight text %}
DEPTNO CNT
------ ----------
    10 ***
    20 *****
    30 ******
{% endhighlight %}

- DB2

  {% highlight sql linenos %}
  select deptno,
         repeat('*',count(*)) cnt
    from emp
   group by deptno
  {% endhighlight %}

- Oracle, PostgreSQL, and MySQL

  {% highlight sql linenos %}
  select deptno,
         lpad('*',count(*),'*') as cnt
    from emp
   group by deptno
  {% endhighlight %}

- SQL Server

  {% highlight sql linenos %}
  select deptno,
	       replicate('*',count(*)) cnt
	  from emp
	 group by deptno
  {% endhighlight %}

#### 创建纵向直方图

例如：

{% highlight text %}
D10 D20 D30
--- --- ---
        *
    *   *
    *   *
*   *   *
*   *   *
*   *   *
{% endhighlight %}

- DB2, Oracle, and SQL Server

  {% highlight sql linenos %}
  select max(deptno_10) d10,
         max(deptno_20) d20,
         max(deptno_30) d30
    from (
  select row_number( )over(partition by deptno order by empno) rn,
         case when deptno=10 then '*' else null end deptno_10,
         case when deptno=20 then '*' else null end deptno_20,
         case when deptno=30 then '*' else null end deptno_30
    from emp
          ) x
    group by rn
    order by 1 desc, 2 desc, 3 desc

  {% endhighlight %}

- PostgreSQL and MySQL

  {% highlight sql linenos %}
  select max(deptno_10) as d10,
         max(deptno_20) as d20,
         max(deptno_30) as d30
    from (
  select case when e.deptno=10 then '*' else null end deptno_10,
         case when e.deptno=20 then '*' else null end deptno_20,
         case when e.deptno=30 then '*' else null end deptno_30,
         (select count(*) from emp d
           where e.deptno=d.deptno and e.empno < d.empno ) as rnk
     from emp e
          ) x
    group by rnk
    order by 1 desc, 2 desc, 3 desc
  {% endhighlight %}


### 分层查询

#### 创建表的分层视图

- DB2 and SQL Server

  {% highlight sql linenos %}
   with x (ename,empno)
      as (
  select cast(ename as varchar(100)),empno
    from emp
   where mgr is null
   union all
  select cast(x.ename||' - '||e.ename as varchar(100)),
         e.empno
    from emp e, x
    where e.mgr = x.empno
   )
   select ename as emp_tree
     from x
    order by 1
  {% endhighlight %}

- Oracle

  {% highlight sql linenos %}
  select ltrim(
	         sys_connect_by_path(ename,' - '),
	       ' - ') emp_tree
	  from emp
	  start with mgr is null
	connect by prior empno=mgr
	  order by 1
  {% endhighlight %}

- PostgreSQL

  {% highlight sql linenos %}
 select emp_tree
   from  (
 select ename as emp_tree
   from  emp
  where mgr is null
 union
 select a.ename||' - '||b.ename
   from emp a
        join
         emp b on (a.empno=b.mgr)
   where a.mgr is null
  union
  select rtrim(a.ename||' - '||b.ename
                      ||' - '||c.ename,' - ')
    from emp a
         join
         emp b on (a.empno=b.mgr)
         left join
         emp c on (b.empno=c.mgr)
   where a.ename = 'KING'
  union
  select rtrim(a.ename||' - '||b.ename||' - '||
               c.ename||' - '||d.ename,' - ')
    from emp a
         join
         emp b on (a.empno=b.mgr)
         join
         emp c on (b.empno=c.mgr)
         left join
         emp d on (c.empno=d.mgr)
   where a.ename = 'KING'
         ) x
   where tree is not null
   order by 1
  {% endhighlight %}

  - Oracle

    {% highlight sql linenos %}
   select emp_tree
    from (
 	 select ename as emp_tree
    from emp
   where mgr is null
 	 union
 	 select concat(a.ename,' - ',b.ename)
    from emp a
         join
 	        emp b on (a.empno=b.mgr)
 	  where a.mgr is null
 	 union
 	 select concat(a.ename,' - ',
 	               b.ename,' - ',c.ename)
 	   from emp a
 	        join
 	        emp b on (a.empno=b.mgr)
 	        left join
 	        emp c on (b.empno=c.mgr)
 	  where a.ename = 'KING'
 	 union
 	 select concat(a.ename,' - ',b.ename,' - ',
 	               c.ename,' - ',d.ename)
 	   from emp a
 	        join
 	        emp b on (a.empno=b.mgr)
 	        join
 	        emp c on (b.empno=c.mgr)
 	        left join
 	        emp d on (c.empno=d.mgr)
 	  where a.ename = 'KING'
 	        ) x
 	  where tree is not null
 	  order by 1
    {% endhighlight %}
