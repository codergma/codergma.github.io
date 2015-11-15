---
layout: post
title: Git常用命令速查表
category: 技术
tags: Git
keywords: 
description: 
---

###git clone 某个分支

```
git clone -b release git@192.168.22.100:root/portal.git
git clone默认克隆的是主分支
要想获得其他分支
git checkout  -b release origin/release
```

