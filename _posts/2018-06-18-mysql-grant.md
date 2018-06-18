---
layout: post
title: mysql 设置权限添加删除用户
tags: [mysql]
category: mysql
---
mysql对用户的添加删除和设置对用户的权限。



对user表进行操作后不会生效，必须重启mysql或者执行`FLUSH PRIVILEGES`刷新授权表
mysql数据库中的3个权限表：user 、db、 host
## 查看账号信息
查看某一个账号的信息
`select host,user from mysql.user`
`show grants for root@localhost`
## 添加账号
### 1、直接插入表中
`insert into mysql.user(Host,User,Password) values("localhost","user",password("admin888"));`
### 2、通过create添加账号
如果密码为空则登录不需要密码
`create user username identified by 'password';`
`CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';` #本地登录 
`CREATE USER 'username'@'%' IDENTIFIED BY 'password';` #远程登录
`CREATE USER 'username'@'127.0.0.1' IDENTIFIED BY 'password';` #指定ip登录
## 删除账号
删除用户帐号必须以root管理员操作
### 从表中删除
该方法必须执行`FLUSH PRIVILEGES;`刷新授权表
`delete FROM mysql.user where user='username' and host='localhost'; 
flush privileges;FLUSH PRIVILEGES;`
#### 删除匿名账号
`delete from mysql.user where user='';FLUSH PRIVILEGES;`
### 通过drop user删除
drop user命令会删除用户以及对应的权限，执行命令后你会发现mysql.user表、mysql.host表和mysql.db表的相应记录都消失了。
`drop user username`
`drop user username@'%';`
`drop user username@localhost;`
## 修改密码
### 方法一
`set password for ‘root’@‘localhost’ =password(‘admin888');`
### 方法二(使用mysqladmin命令修改)
`shell> mysqladmin -u username -h host_name –p password 'newpwd'`
### 方法三
`UPDATE mysql.user SET Password = PASSWORD('admin888')->WHERE User = 'root';FLUSH PRIVILEGES;`
### 方法四（修改当前登录账号密码）
`SET PASSWORD = PASSWORD(’admin888');`
### 方法5（通过从新授权修改密码）
`GRANT All ON＊.* to 'admin888'@'localhost' IDENTIFIED BY'admin888';`
### 忘记root密码
如果其它密码遗忘使用root账号修改即可
但是如果root密码遗忘就会稍微麻烦一点
#### 步骤一
修改mysql配置文件vim /etc/my.cnf
#### 步骤二
在[mysqld]块中加上skip-grant-tables
意思跳过权限验证
#### 步骤三
重启mysql使配置生效
service mysqld restart
#### 步骤四
使用上面修改密码的方法尽快修改密码
`update mysql.user set password = password('') where user ='root';`
#### 步骤五
删除my.cnf中skip-grant-tables
如果不删除那么mysql就一直处于开发所有权限状态
#### 步骤六
重启mysql使配置文件生效
`service mysqld restart`
## 授权
设置对hepps库的所有权限
`Grant all on hepps.* to 'admin888'@'%'`
`Grant all privileges on hepps.* to 'admin888'@'%'`
### ‘%’含义
%表示任意值，以示例表示%代表任意来源
### 添加查询hepps数据库所有表权限
`grant select on hepps.* to admin888@localhost IDENTIFIED BY'admin888';`
### 设置hepps数据库的curd权限
`Grant select,insert,update,delete on hepps.* to admin888@localhost`
#### 注意
如果不添加`IDENTIFIED BY`表示不修改密码
操作完后必须刷新权限表`flush privileges;`或者重启
## 参考链接
百度经验：[MySQL的权限（27种）https://jingyan.baidu.com/article/dca1fa6fb4ca34f1a5405270.html](https://jingyan.baidu.com/article/dca1fa6fb4ca34f1a5405270.html) 