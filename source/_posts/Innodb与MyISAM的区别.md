---
title: "Innodb与MyISAM的区别"
date: 2016-04-13 13:07:59
tags: [数据库,Mysql]
categories: [数据库,Mysql]
---

1.InnoDB不支持FULLTEXT类型的索引。
2.InnoDB 中不保存表的具体行数，也就是说，执行select count(*) from table时，InnoDB要扫描一遍整个表来计算有多少行，但是MyISAM只要简单的读出保存好的行数即可。注意的是，当count(*)语句包含 where条件时，两种表的操作是一样的。
3.对于AUTO_INCREMENT类型的字段，InnoDB中必须包含只有该字段的索引，但是在MyISAM表中，可以和其他字段一起建立联合索引。
4.DELETE FROM table时，InnoDB不会重新建立表，而是一行一行的删除。
5.LOAD TABLE FROM MASTER操作对InnoDB是不起作用的，解决方法是首先把InnoDB表改成MyISAM表，导入数据后再改成InnoDB表，但是对于使用的额外的InnoDB特性(例如外键)的表不适用。
