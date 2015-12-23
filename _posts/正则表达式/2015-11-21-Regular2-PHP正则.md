---
layout: post
title: Regular2: php中正则表达式的应用
category: 技术
tags: Regular
keywords: 
description: 
---
每一种语言对正则表达式的支持有一些细微的差别。

###preg_metch()/preg_metch_all()
>参数pattern, subject, matches		
>>$matches[0] 将包含完整模式匹配到的文本
>>$matches[1] 将包含第一个捕获子组(概念在基础篇中提及)匹配到的文本，以此类推
>两个函数的区别是前者执行非全局匹配（匹配一次即终止），后者执行全局匹配(相当于在正则表达式中使用了g参数)。		

###关于捕获组，即matches[1],matches[2],...
```
$pattern = "/(\d{4})-(\d{2}-(\d\d))/";
$subject = "2010-01-02 2020-03-04";
preg_match_all($pattern, $subject, $matches);
var_dump($matches);

/**输出结果
array(4) {
  [0]=>
  array(2) {
    [0]=>
    string(10) "2010-01-02"
    [1]=>
    string(10) "2020-03-04"
  }
  [1]=>
  array(2) {
    [0]=>
    string(4) "2010"
    [1]=>
    string(4) "2020"
  }
  [2]=>
  array(2) {
    [0]=>
    string(5) "01-02"
    [1]=>
    string(5) "03-04"
  }
  [3]=>
  array(2) {
    [0]=>
    string(2) "02"
    [1]=>
    string(2) "04"
  }
}
*/
```

###关于"?:"
```
$pattern = "/(?:\d{4})-(\d{2}-(\d\d))/";
$subject = "2010-01-02 2020-03-04";
preg_match_all($pattern, $subject, $matches);
var_dump($matches);
#没有输出年份的捕获组
array(3) {
  [0]=>
  array(2) {
    [0]=>
    string(10) "2010-01-02"
    [1]=>
    string(10) "2020-03-04"
  }
  [1]=>
  array(2) {
    [0]=>
    string(5) "01-02"
    [1]=>
    string(5) "03-04"
  }
  [2]=>
  array(2) {
    [0]=>
    string(2) "02"
    [1]=>
    string(2) "04"
  }
}

```

###preg_replace()/preg_filter
>除了返回值有区别外，其余相同，执行搜索和替换
>参数$pattern, $replacement, $subject

###php中正则表达式的反向引用
>捕获组捕获到的内容，不仅可以在正则表达式外部通过程序进行引用，也可以在正则表达式内部进行引用，这种引用方式就是反向引用
```
$pattern = "/(\w+),(\d+),(\w+)/";
$replacement = '${3}000$2$1'; 如果是双引号需要这样写"\${3}000$2$1"
$subject = "abc,1111,def,test,aaa";
$result = preg_replace($pattern,$replacement,$subject);
var_dump($result);
```

###其他
-在正则表达式中匹配反斜杠(\),需要这样"\\\\",一次是在字符串中转义,一次是在正则表达式中转义