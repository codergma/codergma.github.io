---
layout: post
title: 2.PHP依赖管理工具Composer	
category: 技术
tags: PHP
keywords: 
description: 
---
###Packagist
```
packagist 是 Composer 的主要资源库;

```

###安装
```
curl -sS https://getcomposer.org/installer | php
mv composer.phar /usr/local/bin/composer

```

###使用
```
#安装依赖，如果存在composer.lock，将会使用composer.lock，如果不存在将会使用composer.json
composer install
#更新依赖，使用composer.json文件，并将更新composer.lock
php composer.phar update

```

###composer.json
```
{
	"require":{
		"供应商名称/项目名称":"版本号"
		...
	}
}
```


###自动加载
```
require 'vendor/autoload.php';

```

###使用中国全量镜像
```
composer config -g repositories.packagist composer http://packagist.phpcomposer.com

```

###php-cli 开启xdebug扩展影响composer的速度
```
#关闭xdebug扩展
;zend_extension=xdebug.so

```

