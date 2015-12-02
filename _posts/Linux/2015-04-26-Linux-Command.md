---
layout: post
title: Linux常用命令
category: 技术
tags: Linux
keywords: 
description: 
---

###wc (Word Count)

```

wc [-cmwlL] filename 
-c:统计字节数
-m:统计字符数
-w:统计字数
-l:统计行数
-L:打印最长行内容
```

###grep
```

grep [-acinvw]  string filename
-a:将binary文件以text文件方式查找数据
-c:计算匹配次数　
-i:忽略大小写
-n:输出行号
-v:反向选择
-r:递归
-w:匹配完整单词
-E:使用可扩展的正则表达式
```

###lsof (List Open File)

```

#lsof 是linux下一个非常实用的系统级的监控和诊断工具．
lsof filename　   : 查找某个文件相关的进程
lsof -g group    : 某个用户组打开的文件信息
lsof -u username : 查找某个用户打开的文件信息
lsof -c process  : 查找某个进程(名字)打开的文件
lsof -p num      : 通过某个进程号(id)显示该进程打开的文件
lsof -i          : 列出所有网络连接
lsof -i tcp      : 列出所有tcp连接
lsof -i udp      : 列出所有udp连接
lsof -i :num     : 列出那个进程使用指定端口
lsof -a          : and 满足多个条件
lsof -o          : or 　满足其中一个,默认
```

###ps(process status)
```

#五种状态码
D不可中断
R运行
S中断
T停止
Z僵死
#参数
a 显示所有进程
u 指定用户的所有进程
-aux  显示所有包含其他使用者的进程
f 显示程序间的关系
```
