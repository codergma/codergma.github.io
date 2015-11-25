---
layout: post
title: Linux　Command
category: 技术
tags: Linux
keywords: 
description: 
---

###wc Word Count

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

grep [-acinv]  string filename
-a:将binary文件以text文件方式查找数据
-c:计算匹配次数　
-i:忽略大小写
-n:输出行号
-v:反向选择
```