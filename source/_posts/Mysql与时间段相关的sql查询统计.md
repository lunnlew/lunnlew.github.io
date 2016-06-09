---
title: "Mysql与时间段相关的sql查询统计"
date: 2016-04-13 13:07:59
tags: [数据库,Mysql]
categories: [数据库,Mysql]
---

[time_field]字段的存储类型是DATETIME类型或者TIMESTAMP类型
[table]表示表名
### 今天
``` sql
    select * from [table] where to_days([time_field]) = to_days(now())
```
### 昨天
``` sql
    select * from [table] where to_days(now())-to_days([time_field]) <= 1
```
### N天
``` sql
    select * from [table] where to_days(now())-to_days([time_field]) <= N
```
### 近7天
``` sql
    select * from [table] where date_sub(curdate(),INTERVAL 7 DAY) <= date([time_field])
```
### 近30天
``` sql
    select * from [table] where date_sub(curdate(),INTERVAL 30 DAY) <= date([time_field])
```
### 本月
``` sql
    select * from [table] where date_format([time_field], '%Y%m') = date_format(curdate() , '%Y%m')
```
### 上月
``` sql
    select * from [table] where period_diff(date_format(now(), '%Y%m'),date_format([time_field], '%Y%m')) = 1
```
### 更细粒度的查询方式使用str_to_date
``` sql
    select * from [table] where str_to_date([time_field],'%Y-%m-%d %H:%i:%s')>='2012-06-28 08:00:00' and str_to_date([time_field],'%Y-%m-%d %H:%i:%s')<='2012-06-28 09:59:59'
```


### 按年汇总，统计:
``` sql
	select sum(mymoney) as totalmoney, count(*) as sheets from [table] group by date_format([time_field], '%Y')
```
### 按月汇总，统计:
``` sql
	select sum(mymoney) as totalmoney, count(*) as sheets from [table] group by date_format([time_field], '%Y-%m')
```
### 按季度汇总，统计:
``` sql
	select sum(mymoney) as totalmoney,count(*) as sheets from [table] group by concat(date_format([time_field], '%Y'),FLOOR((date_format([time_field], '%m')+2)/3))
```
### 按小时:
``` sql
	select sum(mymoney) as totalmoney,count(*) as sheets from [table] group by date_format([time_field], '%Y-%m-%d %H ')
```
### 查询本年度的数据:
``` sql
	select * FROM [table] WHERE year([time_field]) = year(curdate())
```
### 查询数据附带季度数:
``` sql
	select id, quarter([time_field]) FROM [table]
```
### 查询本季度的数据:
``` sql
	select * FROM [table] WHERE quarter([time_field]) = quarter(curdate())
```
### 本月统计:
``` sql
	select * from [table] where month([time_field]) = month(curdate()) and year([time_field]) = year(curdate())
```
### 本周统计:
``` sql
	select * from [table] where month([time_field]) = month(curdate()) and week([time_field]) = week(curdate())
```
