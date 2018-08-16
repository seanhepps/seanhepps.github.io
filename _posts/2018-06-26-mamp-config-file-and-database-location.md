---
layout: post
title: mamp 配置文件已经数据库位置
tags: [mamp]
category: mamp
---
MAMP mac集成环境套装,配置文件已经数据库储存位置。


经过多时的查找终于找到了`MAMP`在mac上面的储存位置：  
`/Library/Application Support/appsolute/MAMP PRO/`  
在Mac中进入该目录需要添加`\`转义空格  
`cd /Library/Application\ Support/appsolute/MAMP\ PRO/`

MAMP所用的配置文件、数据库文件都在该目录，包括phpMyAdmin.  
不过更改这个文件夹里面的配置文件是无效的，因为在每次服务重新重启的时候，会重新生成配置文件.

## 如何手动修改MAMP的配置
`/Applications/MAMP PRO/MAMP PRO.app/Contents/Resources`  
以上路径中的配置文件是模板，只有修改模板文件才会有效，否则修改其它地方的配置文件不是被覆盖就是没有生效。  
注意：要养成先备份的好习惯