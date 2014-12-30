---
layout: post
title: "深刻的教训-SQL Server关于TempDB的使用"
category: other
tags: [Database, 数据库, MSSQL, SQL Server, TempDB, 教训]
comments: true
share: true

---

目录

* Table of Contents
{:toc}

## The usage of mssql tempdb ##

`文/温国兵`

## 场景现象 ##

中午查询了流水，因未与业务人员沟通好，忘了删选条件，导致TempDB不能分配空间，SQL Server高负载运行。

## 错误分析 ##

我们来看看错误日志：

![错误日志](http://i.imgur.com/fwtY0xt.jpg)

再来看看TempDB自增长记录：

![TempDB自增长记录](http://i.imgur.com/exMPjmh.png)

## 导致原因 ##

查询语句未指定删选条件，语句如下：

{% highlight sql %}
--得到流水，因数据敏感问题，已将字段使用’xx’代替。
IF EXISTS (SELECT *
           FROM   tempdb..sysobjects
           WHERE  id = Object_id(N'tempdb..#t_scfw')
                  AND type = 'U')
  DROP TABLE #t_scfw;

IF NOT EXISTS (SELECT *
               FROM   tempdb..sysobjects
               WHERE  id = Object_id(N'tempdb..#t_scfw')
                      AND type = 'U')
  SELECT tsvr.*,
         bsl.xx AS xxx,
         bsl.xx,
         bsl.xx
  INTO   #t_scfw
  FROM   #t1 AS tsvr
         JOIN t2 AS bsl
           ON tsvr.xx = bsl.xx
              AND tsvr.xx = bsl.xx
              AND tsvr.xx = bsl.xx
              AND tsvr.xx = bsl.xx
              AND bsl.xx > 0;
{% endhighlight %}

## 总结 ##

由于tempdb是存储在SSD上，且总大小为270G。所以，在显式使用临时表时一定要注意数据大小。避免把tempdb空间耗尽，影响整个SQLServer的正常运行。好在设置了tempdb的最大空间，并且最大空间小于SSD硬盘的最大容量，不然服务器的盘就会挂掉，从而导致服务器宕机，多么痛的领悟！切忌犯如此低级错误，作下此文提醒和鞭策自己，凡事三思而后行！

–EOF–

原文地址：<a href="http://blog.csdn.net/justdb/article/details/24097741" target="_blank"><img src="http://i.imgur.com/BROigUO.jpg" title="深刻的教训-SQL Server关于TempDB的使用" height="16px" width="16px" border="0" alt="深刻的教训-SQL Server关于TempDB的使用" /></a>

题图来自：原创，By <a href="https://dbarobin.github.io/" target="_blank">Robin Wen</a>

版权声明：自由转载-非商用-非衍生-保持署名<a href="http://creativecommons.org/licenses/by-nc-nd/3.0/deed.zh" target="_blank">（创意共享3.0许可证）</a>

## 作者信息 ##

温国兵

* Robin Wen
* <a href="mailto:dbarobinwen@gmail.com"><img src="http://i.imgur.com/7yOaC7C.png" title="Robin's Gmail" border="0" height="16px" width="16px" alt="Robin's Gmail" /></a>
* <a href="https://github.com/dbarobin" target="_blank"><i class="fa fa-github"></i></a>
* <a href="https://dbarobin.github.io/" target="_blank"><img src="http://i.imgur.com/dEfMkyt.jpg" title="Robin's Blog" border="0" alt="Robin's Blog" height="16px" width="16px" /></a>
* <a href="http://blog.csdn.net/justdb" target="_blank"><img src="http://i.imgur.com/BROigUO.jpg" title="DBA@Robin's CSDN" height="16px" width="16px" border="0" alt="DBA@Robin's CSDN" /></a>