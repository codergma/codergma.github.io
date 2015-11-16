---
layout: post
title: 开发环境部署整理
category: 技术
tags: Linux
keywords: 
description:
---

###VMware Tools
- 点击虚拟机中的安装VMware Tools会自动下载安装包到/media/用户名/VMware目录中,
- 在此目录中是不能解压的，需要移动到家目录下.
- sudo tar -xzvf <filename>  
- sudo ./安装脚本(忘记叫啥了)
- 回车回车，默认配置即可

###安装sublime
- 下载sublime　deb包
-　sudo dpkg -i <filename>
- 按照自己的习惯配置
```
{
	"default_line_ending": "unix",
	"font_size": 16,
	"ignored_packages":
	[
	],
	"tab_size": 4,
	"auto_complete_triggers": [ {"selector": "text.html", "characters": "<"} ],
}
```
###安装搜狗输入法
- 下载sougou deb包
- sudo dpkg -i <filename>
- 安装完成之后先不要急着重启电脑，否则可能会出现循环登录的问题，可能是字符集的问题．
- system -> Language Support -> fcitx
- 点击小企鹅　添加搜狗输入法
- 关于sublime里不能使用搜狗输入法，自行谷歌百度之(http://www.zhuantilan.com/jiqiao/46423.html)

###安装git,vim,curl,wget等常用软件
- sudo apt-get install vim git curl wget -y






