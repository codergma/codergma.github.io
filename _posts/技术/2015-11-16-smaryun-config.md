---
layout: post
title: ubuntu开发环境部署
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

```

#按照自己的习惯配置
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

###安装vim

- sudo apt-get install vim 
- 习惯配置 https://github.com/codergma/MyConfig.git

###安装搜狗输入法

- 下载sougou deb包
- sudo dpkg -i <filename>
- 安装完成之后先不要急着重启电脑，否则可能会出现循环登录的问题，可能是字符集的问题．
- system -> Language Support -> fcitx
- 点击小企鹅　添加搜狗输入法
- 关于sublime里不能使用搜狗输入法，自行谷歌百度之(http://www.zhuantilan.com/jiqiao/46423.html)

###安装git,curl,wget等常用软件
- sudo apt-get install git curl wget -y

###安装LAMP套件

```
sudo apt-get install apache2 mysql-server mysql-client php5-gd php5-mysql phpmyadmin -y
#apache开启重定向
sudo a2enmod rewrite              
#集成应用中心需要php5-curl
sudo apt-get install libcurl3 libcurl3-dev php5-curl
#重启apache
sudo service apache2 restart
```

###安装redis

```
 #源码编译安装
 wget http://download.redis.io/releases/redis-3.0.0.tar.gz
 tar -xzvf redis-3.0.0.tar.gz
 cd redis-3.0.0
 make
 sudo make install
 sudo ./utils/install_server.sh   #执行安装脚本，使用默认设置
 #默认配置为
 Port:				6379
 Config file: 		/etc/redis/6379.conf
 Log    file:		/var/log/redis_6379.log
 Data dir   :       /var/lib/redis/6379
 Executable : 		/usr/local/bin/redis-server
 Cli Executable:    /usr/local/bin/redis-cli
 #启动redis　client查看是否安装成功
 redis-cli 
 quit     　＃退出
```

###安装PHP的Redis扩展

```
git clone https://github.com/phpredis/phpredis.git
cd phpredis
sudo apt-get install php5-dev
sudo phpize                   #用来安装php的扩展
./configure
make
sudo make install
sudo vim /etc/php5/apache2/php.ini
添加extension=redis.so
sudo service apache2 restart
```
###Ruby相关概念

- RVM 用于帮你安装Ruby环境，帮你管理多个Ruby环境，帮你管理你开发的每个Ruby应用使用机器上哪个Ruby环境。Ruby环境不仅仅是Ruby本身，还包括依赖的第三方Ruby插件。都由RVM管理.
- RubyGems是一个方便而强大的Ruby程序包管理器,随ruby1.9+安装.
- bundler相当于多个RubyGems批处理运行。在配置文件gemfilel里说明你的应用依赖哪些第三方包，他自动帮你下载安装多个包，并且会下载这些包依赖的包。
- Rails 开发框架
-　Passenger是一个Rails应用服务的管理工具，可以统一管理Rails进程的数量、生命周期、请求队列等等。

###部署Ruby环境

```

curl -L http://get.rvm.io | bash -s stable 
type rvm | head -n 1 		#测试RVM是否安装成功
rvm is a function			#表示安装成功
rvm list know				#列出rvm已知的ruby版本
rvm install 2.0				#选择需要的ruby进行安装
rvm use 2.0					#使用2.0版本,
#(Run command as login shell option is checked under the Title and Command tab in Profile Preferences.)
ruby -v 					#当前运行的ruby版本
rvm use 2.0 --default       #设置某版本为默认版本
```


###安装bundler

```

gem source -l      #查看源, 如果你不能翻墙，那么就换成淘宝镜像
gem source --remove  https://rubygems.org/    #移除官方源
gem source --add     https://ruby.taobao.org/ #添加淘宝镜像
gem install bundler
```

###安装Rails

- 必须安装了ruby        
- 必须安装了RubyGems  &nbsp,&nbsp(ruby1.9+默认集成了)
- SQLite3  &nbsp,&nbsp,&nbsp(类Unix自带sqlite3, sqlite3 --version)

```

gem install rails
sudo apt-get install nodejs #rails需要运行js的环境
rails new blog       		＃创建blog程序
cd blog 
bundle install       		#安装Gemfile中列出的gem
cd blog
rails server         		#启动rails内置服务器
localhost:3000       		#冒烟测试
```

###安装passenger

```

gem install passenger
```

###配置passenger+apache2

```

```


















