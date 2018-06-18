---
layout: post
title: Linux 网站目录文件权限安全设置
tags: [linux]
category: linux
---
linux服务器设置网站目录文件的权限，以使网站更安全


apache的运行用户为apache
nginx和php-fpm运行用户为www
我们的网站html目录所属者为admin用户
## 修改用户组
`chown -R admin:apache /var/www/html`
## 对目录设置750权限
750 admin用户对目录有绝对的控制权 其它用户没有控制权 服务器只能读取和执行

`find -type d -exec chmod 750 {} \;`
## 对文件设置640权限
640 admin用户可以对文件进行读和写 服务器只能读取

`find -not -type d -exec chmod 640 {} \;`
## 针对特殊目录给与写入权限
针对个别目录设置可写权限。比如网站的一些缓存目录就需要给web服务有写入权限。例如discuz的/data/目录就必须要写入权限。

`find data -type d -exec chmod 770 {} \;`