---
layout: post
title: certbot命令选项大全
tags: [https,ca,certbot]
category: https
---
介绍certbot命令行选项，完整命令行选项翻译版。


Certbot支持很多命令行选项。以下是完整列表，使用 ：`certbot --help all` 
``` 
用法:  
certbot [子命令] [选项] [-d 域名] [-d 域名] ...
Certbot工具用于获取和安装 HTTPS/TLS/SSL 证书(专门为了Let's encrypt设计)。默认情况下，Certbot会尝试为本地服务器获取并安装证书。  
获取, 安装, 更新证书:  
(默认) run       运行获取并安装当前网络服务器中的证书  
certonly        获取或更新证书，但是不安装    
renew           更新所有先前获得并在一个月之内过期的证书   
enhance         将安全增强功能添加到现有配置  
-d DOMAINS      指定证书对应的域名列表，域名之间使用逗号分隔  
--apache        使用Apache插件进行身份认证和安装  
--standalone    运行一个独立的网页服务器用于身份认证  
--nginx         使用Nginx插件进行身份认证和安装  
--webroot       将文件放置在网站根目录中以进行身份​​验证  
--manual        使用交互式或脚本钩子的方式获取证书  
  
  -n                非交互式运行，多用于cron计划任务，不会进行任何询问
  --test-cert       从测试服务器获取测试证书
  --dry-run         测试“更新”或“认证”但是不存储到本地硬盘  
  
证书管理:    
    certificates    显示使用Certbot生成的所有证书的信息  
    revoke          撤销证书(supply --cert-path指定证书文件的路径)  
    delete          删除证书 先撤销在删除  
    
使用Let's Encrypt管理帐户：  
  register          创建一个Let's Encrypt ACME帐户  
  --agree-tos       同意ACME服务器的订阅协议  
   -m EMAIL         接收重要帐户通知的电子邮件地址  
   
可选参数:  
-h, --help          显示帮助信息，然后退出（后面加上all选项会显示所有帮助信息）
-c或--config         配置文件配置文件的路径 (默认: /etc/letsencrypt/cli.ini或 ~/.config/letsencrypt/cli.ini)  
-v, --verbose       当前参数可以重复使用多次来增加输出信息的详细程度，例如 -vvv.
                        (默认: -2)  
--max-log-backups MAX_LOG_BACKUPS 
                    指定备份日志的最大数量，应该由Certbot内置的日志循环来保存。将此标志设置为0将完全禁用日志循环，导致Certbot始终追加到相同的日志文件。（默认：1000）  
-n                  非交互式，无需询问用户输入即可运行。这可能需要添加额外的命令选择以确保执行过程中不需要询问用户; 客户会尝试解释哪些是必需的，如果它找到一个缺失（默认：False）  
--force-interactive 无论Certbot是否以命令行的方式运行，强制交互式运行。当前参数不能用于renew子命令。(默认: False)  
-d                  指定域名列表。如果有多个域名，可以多次使用-d参数，也可以在-d参数后使用逗号分隔的域名列表。提供的第一个域名将成为证书的subject CN和全部域名将成为主题替代名称证书。第一个域也将用于一些软件用户界面和文件路径对于证书和相关材料除外否则指定或您已经有证书同名。在名称相撞的情况下会在文件路径名称后附加一个数字，如0001。（默认：询问）  
--cert-name         要应用的CERTNAME证书名称。这个名字被Certbot使用在文件路径中国; 它没有 影响证书本身的内容。查看证书名称，运行'certbot certificates'。在创建一个新证书的时候，指定新的证书的名称。（默认：创建证书时列出的域名的第一个）  
--dry-run           使用客户端执行一次试运行，获取测试证书(无效的证书)但不保存到磁盘。当前选项仅用于'certonly'和'renew'子命令。 注: 尽管 --dry-run 选项试图阻止任何对系统的修改，但并不能做到完全避免: 如果使用类似apache或nginx网页服务器来认证插件，程序运行过程中，会尝试修改或恢复配置文件来获取测试证书，也会重启网页服务器来部署和回滚这些修改。如果定义了 --pre-hook 和--post-hook 选项它们会被同时执行，这两个选项有助于更精确地模拟更新证书。--renew-hook 选项在这里不会被执行。(默认: False)  
--debug-challenges  设置验证后，在提交给CA之前等待用户输入（默认：False）  
--preferred-challenges
                    一个经过排序的逗号分隔的首选列表在验证期间使用验证最多首先列出首选验证方式（例如，“dns”或“tls-sni-01，http，dns“）。并非所有的插件都支持验证方式。看到[https://certbot.eff.org/docs/using.html#plugins](https://certbot.eff.org/docs/using.html#plugins)。ACME验证是会根据验证方式选择版本的，但如果你 选择“http”而不是“http-01”，Certbot会选择最新版本自动。（默认：[]）  
--user-agent        用户代理设置本客户端的用户代理信息。用户代理信息用于CA机构收集关于操作系统和插件的使用成功率。如果你希望隐藏此信息，设置此选项为""。(默认: CertbotACMEClient/0.24.0 (certbot;darwin 10.13.4) Authenticator/XXX Installer/YYY(SUBCOMMAND; flags: FLAGS) Py/2.7.14)  
--user-agent-comment
                    用户代理评论 。在重新打包Certbot或从中调用时使用另一个工具来允许额外的统计数据被收集。如果已设置--user-agent则忽略。（例如：Foo-Wrapper / 1.0）（默认值：无）  
                    
自动化:  
用于自动运行或其他情况的参数  
--keep-until-expiring, --keep, --reinstall
                            如果被请求的证书已经存在，那么不执行更新操作直到证书将要过期(如果使用了'run'子命令，无论是否过期证书都会被更新)。(默认: 询问)  
 --expand                   如果请求的证书名字是已经存在的证书名字的子集，那么这个本地证书会被重置并重命名。(默认: 询问)  
 --version                  显示程序和版本号，然后退出  
 --renew-with-new-domains   如果被请求的证书已经存在，但是域名变了，那么无论该证书是否将要过期都会被更新。(默认: False)  
 --allow-subset-of-names    当执行域名验证时，如果不能对所有子集获得授权，则不认为它是失败的。这可能有助于允许多个域名的更新成功，即使某些域名不再指向该网站。此选项不能与--csr起使用。（默认值：false）  
 --agree-tos                同意ACME订阅协议 (默认: 询问)  
 --duplicate                允许制作与现有副本重复的证书谱系（两者可以并行更新）  
 --os-packages-only         (仅用于 certbot-auto) 安装系统依赖包，然后停止 (默认: False)  
 --no-self-upgrade          (仅用于 certbot-auto) 禁止 certbot-auto 脚本自动升级自己到新的发布版本 (默认: 自动升级)  
 --no-bootstrap             (仅限  certbot-auto）阻止certbot-auto脚本安装操作系统级的依赖项（默认：提示安装操作系统范围的依赖项，但如果用户说'否'则退出）  
 -q, --quiet                程序运行只输出错误信息。这个选项对于 cron 等自动化工具很有用。 该选项默认包含了 --non-interactive 选项的功能。(默认: False) 
  
安全:  
有关安全的参数和服务器设置  
 
--rsa-key-size N        RSA密钥的大小。 (默认: 2048)  
--must-staple           为证书添加 OCSP Must Staple 扩展。当Apache版本高于2.3.3时，自动配置 OCSP Stapling 支持。 (默认: False)  
--redirect              自动将所有HTTP通信重定向到HTTPS新认证的虚拟主机。（默认：询问）  
--no-redirect           不要自动将所有HTTP流量重定向到最新验证的虚拟主机的HTTPS。 （默认：询问）
--hsts                  将Strict-Transport-Security头添加到每个HTTP响应。 强制浏览器始终对域名使用SSL。 防范SSL剥离。 （默认：无）
--uir                   将“Content-Security-Policy：upgrade-insecure-requests”标头添加到每个HTTP响应中。 强制浏览器对每个http：//资源使用https：//。 （默认：无）
--staple-ocsp           启用OCSP装订。 一个有效的OCSP响应被装订到服务器在TLS期间提供的证书中。 （默认：无）
--strict-permissions    要求所有配置文件都由当前用户拥有; 只有当你的配置文件在某些不安全地方时需要就像/tmp/（默认：False）  

测试:  
以下选项仅用于测试和集成目的。  
--test-cert, --staging  使用演示服务器获取或撤销（无效）证书; 相当于--server https：//acme-staging-v02.api.letsencrypt.org/directory（默认值：False）  
--debug                 在出现错误时显示回溯，并允许在实验平台上执行certbot-auto（默认值：False）  
--no-verify-ssl         禁用验证ACME服务器的证书。 （默认：False）  
--tls-sni-01-address TLS_SNI_01_ADDRESS 
                        tls-sni-01验证期间服务器侦听的地址。 （默认：）  
--http-01-port HTTP01_PORT 
                        在http-01验证中使用的端口。 这只影响Certbot侦听的端口。 符合标准的ACME服务器仍会尝试连接端口80.（默认值：80）  
--http-01-address HTTP01_ADDRESS    
                        http-01验证期间服务器侦听的地址。 （默认：）  
--break-my-certs        愿意用无效（测试/分期）证书替换或续订有效证书（默认值：False）

路径:  
更改执行路径和服务器的标志  
--cert-path CERT_PATH           保存证书的路径（with auth --csr），安装或撤消的路径。 （默认：无）  
--key-path KEY_PATH             证书安装或撤销的私钥路径（如果帐户密钥丢失）（默认值：无）  
--fullchain-path FULLCHAIN_PATH 附带完整证书链（证书加链）的路径。 （默认：无）  
--chain-path CHAIN_PATH         证书链的路径。 （默认：无）  
--config-dir CONFIG_DIR         配置目录，（默认：/etc/letsencrypt）  
--work-dir WORK_DIR             工作目录（默认： /var/lib/letsencrypt）  
--logs-dir LOGS_DIR             日志目录（默认：/var/log/letsencrypt）  
--server SERVER                 ACME目录资源URI。 （默认：https：//acme-v01.api.letsencrypt.org/directory）

管理:  
各种子命令和选项可用于管理你的证书：  
certificates    列出由Certbot管理的证书
delete          清理与证书相关的所有文件 （注意最好先注销在删除）  
renew           续订所有证书（或使用--cert-name） 
revoke          撤消使用--cert-path指定的证书(证书的存放路径)
update_symlinks 重新创建/etc/letsencrypt/live/目录中的符号链接

run:  
获取和安装证书的选项  
certonly：       修改如何获取证书的选项  
    --csr CSR    DER或PEM格式的证书签名请求（CSR）路径。 目前--csr只适用于'certonly'子命令。 （默认：无）  

renew:  
  '更新'子命令将尝试更新您以前获得的所有证书（或更准确地说，证书谱系）（如果它们即将到期），并打印结果摘要。 默认情况下，'renew'将重用用于创建获取或最近成功续订每个证书沿袭的选项。 你可以先用`--dry-run`试试。 对于更细粒度的控制，您可以使用`certonly`子命令续订个体谱系。 钩子可用于在更新之前和之后运行命令; 请参阅https://certbot.eff.org/docs/using.html#renewal 更多关于这些的信息。
    --pre-hook PRE_HOOK         命令在获取任何证书之前在shell中运行。 主要用于更新，可用于暂时关闭可能与独立插件冲突的网络服务器。 只有在实际获得/更新证书的情况下才会调用此功能。 更新多个具有相同预挂钩的证书时，只会执行第一个。 （默认：无）  
    --post-hook POST_HOOK       尝试获取/更新证书后，在shell中运行的命令。 可用于部署更新的证书，或重新启动任何由--pre-hook停止的服务器。 只有在尝试获取/更新证书时才会执行此操作。 如果多个更新的证书具有相同的post-hook，则只会运行一个证书。 （默认：无）  
    --deploy-hook DEPLOY_HOOK   命令在每个成功颁发的证书的shell中运行一次。 对于这个命令，shell变量$RENEWED_LINEAGE将指向包含新证书和密钥的config live子目录（例如“/etc/letsencrypt/live/example.com”）; shell变量$RENEWED_DOMAINS将包含空格分隔的更新证书域列表（例如，“example.com www.example.com”（默认值：无）  
    --disable-hook-validation   通常为--pre-hook/--post-hook/--deploy-hook指定的命令将检查其有效性，以查看正在运行的程序是否位于$PATH中，以便可以及早发现错误 当钩子尚未运行时。 验证过于简单，如果使用更高级的shell构造，则验证失败，因此您可以使用此开关来禁用它。 （默认：False）  
    --no-directory-hooks        在更新期间禁用在Certbot的钩子目录中找到的正在运行的可执行文件。 （默认：False）  
    
certificates:  
    列出由Certbot管理的证书 
     
delete: 删除证书的选项  

revoke: 撤销证书的选项  
    --reason                    {unspecified，keycompromise，affiliationchanged，superseded，cessationofoperation}指定吊销证书的理由。 （默认：未nspecified）  
    --delete-after-revoke       撤销证书后删除证书。 （默认：none）  
    --no-delete-after-revoke    撤销证书后不要删除它们。 此选项应谨慎使用，因为'renew'子命令将尝试更新未删除的已吊销证书。 （默认：无）  

register: 账户注册和修改选项  
    --register-unsafely-without-email   指定此标志可以注册一个没有电子邮件地址的帐户。 强烈建议不要这样做，因为如果发生重大损失或帐户损害，您将无法撤销对您帐户的访问权限。 您也将无法收到即将到期或撤销证书的通知。 订阅者协议的更新仍然会对您产生影响，并将在发布网站更新14天后生效。 （默认：False）  
    --update-registration               更新注册信息，表示应该更新与现有注册相关的详细信息，例如电子邮件地址，而不是注册新帐户。 （默认：False）  
    -m EMAIL, --email EMAIL             用于注册和恢复联系人的电子邮件。（默认：ask）  
    --eff-email                         与EFF分享您的电子邮件地址（默认：none） 
    --no-eff-email                      不要与EFF分享您的电子邮件地址（默认值：none） 
 
unregister:     帐户停用的选项。
    --account ACCOUNT_ID    要使用的帐户ID（默认值：none）  

install:        用于修改证书部署方式的选项  

config_changes: 控制显示哪些更改的选项  
    --num NUM               您想要显示多少个过去的修订版本（默认值：none）  

rollback:       回滚服务器配置更改的选项  
    --checkpoints N         恢复配置N个检查点。（默认值：1）  
 
plugins:        “plugins”子命令的选项  
    --init                  初始化插件。（默认：False）  
    --prepare               初始化并准备插件。（默认：False）  
    --authenticators        仅限于验证程序插件。（默认：无）  
    --installers            仅限于安装程序插件。（默认：无）  
    
update_symlinks：更新符号链接 如果您在/etc/letsencrypt/live中重新创建证书和密钥符号链接
  手动更改它们或编辑更新配置文件  

enhance：        通过将安全增强功能添加到已有的配置来帮助强化TLS配置。  

plugins:        插件选择：Certbot客户端支持可扩展的插件架构。 请参阅“certbot插件”以获取所有安装的插件及其名称的列表。 您可以通过设置下面提供的选项来强制某个特定的插件。 正在运行--help <plugin_name>将列出特定于该插件的标志。   
    --configurator CONFIGURATOR
                    同时是认证者和安装者的插件的名称。 不应与--authenticator或--installer一起使用。 （默认：询问）  
    -a AUTHENTICATOR, --authenticator AUTHENTICATOR 
                    身份验证器插件名称。 （默认：none）  
    -i INSTALLER, --installer INSTALLER 
                    安装程序插件名称（也用于查找域）。（默认：none）  
    --apache        使用Apache获取并安装证书（默认值：False）  
    --nginx         使用Nginx获取并安装证书（默认值：False）  
    --standalone    使用“standalone”网络服务器获取证书。（默认值：False）  
    --manual        使用手动方式获取证书（默认值：False）  
    --webroot       通过将文件放入网站根目录获取证书。 （默认：False）  
    
    DNS方式验证：需要配置DNS方式验证所需要的两个参数。  
        1、 --dns-dnsname-propagation-seconds 在要求ACME服务器验证DNS记录之前等待DNS传播的秒数  
        2、 --dns-dnsname-credentials         Dns凭证配置文件  
        --dns-cloudflare    使用DNS TXT记录获取证书（如果您使用Cloudflare作为DNS）。 （默认：False）参数1、10 参数2、None  
        --dns-cloudxns      使用DNS TXT记录获取证书（如果您使用CloudXNS进行DNS）。 （默认：False）参数1、30 参数2、None   
        --dns-digitalocean  使用DNS TXT记录获取证书（如果您使用DigitalOcean for DNS）。 （默认：False）参数1、10 参数2、None   
        --dns-dnsimple      使用DNS TXT记录获取证书（如果您使用DNSimple进行DNS）。 （默认：False）参数1、30 参数2、None   
        --dns-dnsmadeeasy   使用DNS TXT记录获取证书（如果您使用的DNS是Made Easy）。 （默认：False）参数1、60 参数2、None   
        --dns-google        使用DNS TXT记录获取证书（如果您使用的是Google Cloud DNS）。 （默认：False）参数1、60 参数2、None   
        --dns-luadns        使用DNS TXT记录获取证书（如果您使用的是DNS的LuaDNS）。 （默认：False）参数1、30 参数2、None   
        --dns-nsone         使用DNS TXT记录获取证书（如果您使用NS1作为DNS）。 （默认：False）参数1、30 参数2、None   
        --dns-rfc2136       使用DNS TXT记录获取证书（如果您使用的是DNS的BIND）。 （默认：False）参数1、60 参数2、None   
        --dns-route53       使用DNS TXT记录获取证书（如果您使用Route53作为DNS）。 （默认：False）参数1、10 参数2、None 

apache: Apache Web Server插件 - Beta  
    --apache-enmod APACHE_ENMOD         Apache 'a2enmod' 二进制文件的路径。 （默认：none）  
    --apache-dismod APACHE_DISMOD       Apache'a2dismod'二进制文件的路径。（默认：none）  
    --apache-le-vhost-ext APACHE_LE_VHOST_EXT SSL 
                                        vhost配置扩展。 （默认：-le- ssl.conf）  
    --apache-server-root APACHE_SERVER_ROOT 
                                        Apache服务器根目录。 （默认/etc/apache2）  
    --apache-vhost-root APACHE_VHOST_ROOT 
                                        Apache服务器VirtualHost配置根目录（默认值：none)  
    --apache-logs-root APACHE_LOGS_ROOT 
                                        Apache服务器日志目录（默认值：/var/log/apache2）   
    --apache-challenge-location APACHE_CHALLENGE_LOCATION 
                                        challenge的目录路径。 （默认：/etc/apache2/other）   
    --apache-handle-modules APACHE_HANDLE_MODULES 
                                        让安装程序为您启用所需的模块（仅限Ubuntu/Debian）（默认值：False）  
    --apache-handle-sites APACHE_HANDLE_SITES 
                                        让安装程序为您处理启用站点（仅限Ubuntu / Debian）（默认值：False）  

Manual(手动)  
  通过手动配置或自定义shell脚本进行身份验证。 在使用shell脚本时，必须提供一个验证器脚本。 此脚本可用的环境变量取决于挑战类型。 $CERTBOT_DOMAIN将始终包含正在进行身份验证的域。 对于HTTP-01和DNS-01，$CERTBOT_VALIDATION是验证字符串，$CERTBOT_TOKEN是执行HTTP-01质询时请求的资源的文件名。 在执行TLS-SNI-01质询时，$CERTBOT_SNI_DOMAIN将包含ACME服务器期望与其位于的自签名证书一起呈现的SNI名称$CERTBOT_CERT_PATH。 完成TLS握手所需的密钥位于$ CERTBOT_KEY_PATH处。 还可以提供额外的清理脚本，并可以使用附加变量$CERTBOT_AUTH_OUTPUT其中包含从auth脚本输出标准输出。  
    --manual-auth-hook MANUAL_AUTH_HOOK         用于验证是钩子执行的脚本或者路径或命令（默认值：none）  
    --manual-cleanup-hook MANUAL_CLEANUP_HOOK   清理时钩子执行的脚本执行路径或命令（默认值：none） 
    --manual-public-ip-logging-ok               自动允许公共IP日志记录（默认：ask）  
nginx: Nginx Web Server插件 - Alpha  
--nginx-server-root NGINX_SERVER_ROOT           Nginx服务器根目录. (default: /etc/nginx)  
--nginx-ctl NGINX_CTL                           'nginx'二进制文件的路径，用于'configtest'并检索nginx版本号。 （默认：nginx）  

null:
  Null Installer  

standalone:
  分离一个临时的网络服务器  

webroot：
  文件在webroot目录中  
    --webroot-path WEBROOT_PATH, -w WEBROOT_PATH    网站根目录，不同的域名可以指定多个，例如`-w /var/www/example -d example.com -d  www.example.com -w /var/www/thing -d thing.net -d m.thing.net` (default: Ask)  
    --webroot-map WEBROOT_MAP                       使用JSON格式传入域名和路径的，例如：--webroot-map '{"eg1.is,m.eg1.is":"/www/eg1/", "eg2.is":"/www/eg2"}'这个选项是-w和-d的合并形式
```