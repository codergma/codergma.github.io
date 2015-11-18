---
layout: post
title: Git自动更新脚本
category: 技术
tags:　PHP Git Linux
keywords: 
description:
---

服务器上的代码需要频繁的更新，很耗费精力，索性就想写个脚本，让apache调用；本想就几分钟的时间搞定，却发现了不少问题.直接执行脚本没问题，通过exec()函数调用脚本却怎么都不行．

###会不会是脚本有问题

- 直接运行脚本是ok的

###apache 有权限运行脚本吗

- 检查脚本的文件权限
-　php.ini中safe_mode是否为off

###运行其他脚本命令

- 可以运行，说明是因为apache没有更新代码的权限

###将运行apache的用户替换成登陆用户

测试发现可以更新代码,但总不能让当前登陆用户运行apache吧

```

sudo vim /etc/apache2/envvars
APACHE_RUN_USER=当前用户
APACHE_RUN_GROUP=当前用户组
```

###解决方案

- 让apache通过root权限更新代码 sudo git pull origin master
- sudo visudo 添加 www-data ALL=(ALL)NOPASSWD:ALL 避免要求输入密码
- 将root 用户的ssh-key添加到gitlab服务器上






