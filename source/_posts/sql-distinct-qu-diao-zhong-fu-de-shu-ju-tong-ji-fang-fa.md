---
date: 2011-01-20
layout:  post
title:  "sql DISTINCT去掉重复的数据统计方法"
tagline:
categories:
- web
tags:
- sql
---
sql DISTINCT去掉重复的数据统计方法(2009-01-13 15:05:43)转载 标签：sqldistinct杂谈     分类：sql
<br>
SELECT指令让我们能够读取表格中一个或数个栏位的所有资料。这将把所有的资料都抓出，无论资料值有无重复。在资料处理中，我们会经常碰到需要找出表格内的不同资料值的情况。换句话说，我们需要知道这个表格/栏位内有哪些不同的值，而每个值出现的次数并不重要。这要如何达成呢？在sql中，这是很容易做到的。我们只要在SELECT后加上一个DISTINCT就可以了。 DISTINCT的语法如下：
<br>
SELECT DISTINCT "栏位名"
<br>
FROM "表格名"
<br>
举例来说，若要在以下的表格，Store_Information，找出所有不同的店名时，Store_Information 表格
<br>
store_name
<br>
Sales
<br>
Date
<br>
1
<br>
$1500
<br>
Jan-05-1999
<br>
2
<br>
$250
<br>
Jan-07-1999
<br>
1
<br>
$300
<br>
Jan-08-1999
<br>
3
<br>
$700
<br>
Jan-08-1999
<br>
我們就鍵入，

    SELECT DISTINCT store_name FROM Store_Information

結果:
<br>
1
<br>
2
<br>
3
<br>
DISTINCT 关键字可从 SELECT 语句的结果中除去重复的行。如果没有指定 DISTINCT，那么将返回所有行，包括重复的行。

    select count(distinct t.destaddr) from nbyd_send t where t.input_time > to_date('2007-2-1','yyyy-mm-dd') and t.input_time < to_date('2007-3-1','yyyy-mm-dd')

可以统计出一个月中的用户数量。
<br>
关于如何快速得知里面每一个号码重复的个数问题的解答:
<br>
利用分组函数的sql语句

    select t.tel,count(*) from nbyd_deliver t group by t.tel ;

group by 解决重复数据的个数统计
<br>

适用于各种关系型数据库,如oracle,sql Server
<br>

查询重复的数据

    select * from (select v.xh,count(v.xh) num from sms.vehicle v group by v.xh) where num>1;--169
    select v.xh,count(v.xh) num from sms.vehicle v group by v.xh having count(v.xh)=2;


删除重复的数据

    create table mayong as (select distinct* from sms.vehicle);
    delete from sms.vehicle ;
    insert into sms.vehicle select * from mayong;

在oracle中，有个隐藏了自动rowid，里面给每条记录一个唯一的rowid，我们如果想保留最新的一条记录，我们就可以利用这个字段，保留重复数据中rowid最大的一条记录就可以了。
<br>

下面是查询重复数据的一个例子：

    select a.rowid,a.* from 表名 a
    where a.rowid !=
    (
    select max(b.rowid) from 表名 b
    where a.字段1 = b.字段1 and
    a.字段2 = b.字段2
    )

下面我就来讲解一下，上面括号中的语句是查询出重复数据中rowid最大的一条记录。
<br>

而外面就是查询出除了rowid最大之外的其他重复的数据了。
<br>
由此，我们要删除重复数据，只保留最新的一条数据，就可以这样写了：

    delete from 表名 a
    where a.rowid !=
    (
    select max(b.rowid) from 表名 b
    where a.字段1 = b.字段1 and
    a.字段2 = b.字段2
    )

随便说一下，上面语句的执行效率是很低的，可以考虑建立临时表，讲需要判断重复的字段、rowid插入临时表中，然后删除的时候在进行比较。

    create table 临时表 as
    select a.字段1,a.字段2,MAX(a.ROWID) dataid from 正式表 a GROUP BY a.字段1,a.字段2;
    delete from 表名 a
    where a.rowid !=
    (
    select b.dataid from 临时表 b
    where a.字段1 = b.字段1 and
    a.字段2 = b.字段2
    );
    commit;

二、对于完全重复记录的删除
<br>

对于表中两行记录完全一样的情况，可以用下面语句获取到去掉重复数据后的记录：

    select distinct * from 表名
    可以将查询的记录放到临时表中，然后再将原来的表记录删除，最后将临时表的数据导回原来的表中。如下：
    CREATE TABLE 临时表 AS (select distinct * from 表名);
    drop table 正式表;
    insert into 正式表 (select * from 临时表);
    drop table 临时表;

如果想删除一个表的重复数据，可以先建一个临时表，将去掉重复数据后的数据导入到临时表，然后在从临时表将数据导入正式表中，如下：
<br>

    INSERT INTO t_table_bak
    select distinct * from t_table;
