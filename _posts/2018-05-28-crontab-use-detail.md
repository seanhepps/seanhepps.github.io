---
layout: posts
title: Linux crontab使用详解
tags: [Linux]
category: linux
---
Linux中crontab计划任务使用详解。


## 基础命令
crontab的核心是crond服务，想要使用crontab需要开启crond服务才行
命令：`service crond start`
启动crond服务后可以使用`crontab`命令对计划任务的命令进行增删改查。
### crontab -e 修改
使用`crontab -e`会进入命令的编辑界面，如果文件不存在就会创建新文件
### crontab -l 列出当前用户的所有计划任务
使用`crontab -l`会列出当前用户所有的计划任务
### crontab -r 删除
`使用crontab -r`会删除当前用的所有的计划任务，因为直接把当前的用户的计划任务文件删掉了
### crontab -ir 删除前提醒
删除crontab文件时提醒该用户
### crontab [-u user] [-r|-l|-e]
查看删除某一个用户的计划任务，必须用户-u的权限才可以
## 用户使用控制
在/etc/cron.allow文件中的用户是可以使用crontab的
在/etc/cron.deny文件中的用户是禁止使用crontab的
## 使用方式
crontab支持两种方式进行计划任务的控制
1、使用命令行的方式通过一系列的命令进行计划任务的增删改查
2、通过目录的方式定时目录可在/etc/crontab中设定。
可以自定义一个文件，编写好计划任务后通过`crontab [file]`命令来提交给crontab
### crond服务
#### 启动服务
service crond start
#### 关闭服务
service crond stop
#### 重启服务
service crond restart
#### 重新载入配置
service crond reload
#### 查看状态
service crond status
## 相关目录
/var/spool/cron/ 目录下存放的是每个用户包括root的crontab任务，每个任务以创建者的名字命名
/etc/crontab 这个文件负责调度各种管理和维护任务。
/etc/cron.d/ 这个目录用来存放任何要执行的crontab文件或脚本。
我们还可以把脚本放在/etc/cron.hourly、/etc/cron.daily、/etc/cron.weekly、/etc/cron.monthly目录中，让它每小时/天/星期、月执行一次。
## 计划任务使用
### 分时年月周
在crontab文件中一个有六个域，前五个是时间后面是要执行的命令
### 特殊符号*、/、-、和,
* 表示所有的取值范围内的数字

/ 代表每的意思,/5表示每5个单位

- 表示区间从某个数字到某个数字

","分开几个离散的数字
### 实例
实例1：每1分钟执行一次command
命令：
* * * * * command

实例2：每小时的第3和第15分钟执行
命令：
3,15 * * * * command

实例3：在上午8点到11点的第3和第15分钟执行
命令：
3,15 8-11 * * * command

实例4：每隔两天的上午8点到11点的第3和第15分钟执行
命令：
3,15 8-11 */2 * * command

实例5：每个星期一的上午8点到11点的第3和第15分钟执行
命令：
3,15 8-11 * * 1 command

实例6：每晚的21:30重启smb 
命令：
30 21 * * * /etc/init.d/smb restart

实例7：每月1、10、22日的4 : 45重启smb 
命令：
45 4 1,10,22 * * /etc/init.d/smb restart

实例8：每周六、周日的1 : 10重启smb
命令：
10 1 * * 6,0 /etc/init.d/smb restart

实例9：每天18 : 00至23 : 00之间每隔30分钟重启smb 
命令：
0,30 18-23 * * * /etc/init.d/smb restart

实例10：每星期六的晚上11 : 00 pm重启smb 
命令：
0 23 * * 6 /etc/init.d/smb restart

实例11：每一小时重启smb 
命令：
* */1 * * * /etc/init.d/smb restart

实例12：晚上11点到早上7点之间，每隔一小时重启smb 
命令：
* 23-7/1 * * * /etc/init.d/smb restart

实例13：每月的4号与每周一到周三的11点重启smb 
命令：
0 11 4 * mon-wed /etc/init.d/smb restart

实例14：一月一号的4点重启smb 
命令：
0 4 1 jan * /etc/init.d/smb restart

实例15：每小时执行/etc/cron.hourly目录内的脚本
命令：
01   *   *   *   *     root run-parts /etc/cron.hourly
## 注意事项
脚本中涉及文件路径时写全局路径
在crontab中%是有特殊含义的，表示换行的意思。如果要用的话必须进行转义\%，如经常用的date ‘+%Y%m%d’在crontab里是不会执行的，应该换成date ‘+\%Y\%m\%d’。
每条任务调度执行完毕，系统都会将任务输出信息通过电子邮件的形式发送给当前系统用户，这样日积月累，日志信息会非常大，可能会影响系统的正常运行，因此，将每条任务进行重定向处理非常重要。
例如，可以在crontab文件中设置如下形式，忽略日志输出：
0 */3 * * * /usr/local/apache2/apachectl restart >/dev/null 2>&1