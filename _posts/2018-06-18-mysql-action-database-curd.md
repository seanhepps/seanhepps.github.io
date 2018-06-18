---
layout: post
title: mysql 对数据库增删改查
tags: [mysql]
category: mysql
---
mysql数据库常用的增删改查操作


## 创建数据库
### 创建utf8字符集
如下脚本创建数据库yourdbname，并制定默认的字符集是utf8。
`CREATE DATABASE IF NOT EXISTS yourdbname DEFAULT CHARSET utf8 COLLATE utf8_general_ci;`
或者
`CREATE DATABASE IF NOT EXISTS yourdbname DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;`
### 创建gbk字符集
如果要创建默认gbk字符集的数据库可以用下面的sql:
`CREATE DATABASE IF NOT EXISTS yourdbname DEFAULT CHARSET gbk COLLATE gbk_chinese_ci;`
或者
`CREATE DATABASE IF NOT EXISTS yourdbname DEFAULT CHARACTER SET gbk COLLATE gbk_chinese_ci;`
## 修改数据库
最保险的办法就是导出sql`mysqldump -u root -p dbname runoob_tbl > dump.sql`然后新建一个数据库在导入进去。
## 删除数据库
`drop database database_name;`
## 查看数据信息
### 查看当前操作的数据库名
`select database();`
### 查看数据库版本号
`select version();`
### 查看当前用户
`select user();`
### 查看当前数据库版本
`select version();`