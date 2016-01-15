---
layout: post
title: PHP 内核
category: 技术
tags: PHP
keywords: 
description:
---
恩，PHP是世界上最好的语言！！！

###1.php代码的执行
!["php-internal"](/public/img/posts/php/php-inernal-01.png)
###2.SAPI
Server Application Programming Interface 指的是PHP的具体应用的编程接口。是PHP和外部程序的编程接口。

* apache模式
>php5经常需要在apache服务器下运行，一般通过mod_php5模块集成。

* 嵌入式
>嵌入式类似CLI模式，也是SAPI接口的另一种实现。只是目前很少有应用将PHP作为嵌入语言来使用， PHP的强项目前还是在Web开发方面。

* FastCGI
>  CGI全称是“通用网关接口”(Common Gateway Interface)， 它可以让一个客户端，从网页浏览器向执行在Web服务器上的程序请求数据。 CGI描述了客户端和这个程序之间传输数据的一种标准。 CGI的一个目的是要独立于任何语言的，所以CGI可以用任何一种语言编写，只要这种语言具有标准输入、输出和环境变量。 如php，perl，tcl等。 </br>
>  FastCGI是Web服务器和处理程序之间通信的一种协议， 是CGI的一种改进方案，FastCGI像是一个常驻(long-live)型的CGI， 它可以一直执行，在请求到达时不会花费时间去fork一个进程来处理(这是CGI最为人诟病的fork-and-execute模式)。 正是因为他只是一个通信协议，它还支持分布式的运算，即 FastCGI 程序可以在网站服务器以外的主机上执行并且接受来自其它网站服务器来的请求。</br>
>  FastCGI是语言无关的、可伸缩架构的CGI开放扩展，将CGI解释器进程保持在内存中，以此获得较高的性能。 CGI程序反复加载是CGI性能低下的主要原因，如果CGI程序保持在内存中并接受FastCGI进程管理器调度， 则可以提供良好的性能、伸缩性、Fail-Over特性等。	</br>
>一般情况下，FastCGI的整个工作流程是这样的：		
>1. Web Server启动时载入FastCGI进程管理器（IIS ISAPI或Apache Module)
>2. FastCGI进程管理器自身初始化，启动多个CGI解释器进程(可见多个php-cgi)并等待来自Web Server的连接。
>3. 当客户端请求到达Web Server时，FastCGI进程管理器选择并连接到一个CGI解释器。 Web server将CGI环境变量和标准输入发送到FastCGI子进程php-cgi。
>4. FastCGI子进程完成处理后将标准输出和错误信息从同一连接返回Web Server。当FastCGI子进程关闭连接时， 请求便告处理完成。FastCGI子进程接着等待并处理来自FastCGI进程管理器(运行在Web Server中)的下一个连接。 在CGI模式中，php-cgi在此便退出了。

* PHP中的CGI实现
>PHP的CGI实现了Fastcgi协议，是一个TCP或UDP协议的服务器接受来自Web服务器的请求， 当启动时创建TCP/UDP协议的服务器的socket监听，并接收相关请求进行处理。随后就进入了PHP的生命周期： 模块初始化，sapi初始化，处理PHP请求，模块关闭，sapi关闭等就构成了整个CGI的生命周期。
>以TCP为例，在TCP的服务端，一般会执行这样几个操作步骤：
>1. 调用socket函数创建一个TCP用的流式套接字；
>2. 调用bind函数将服务器的本地地址与前面创建的套接字绑定；
>3. 调用listen函数将新创建的套接字作为监听，等待客户端发起的连接，当客户端有多个连接连接到这个套接字时，可能需要排队处理；
>4. 服务器进程调用accept函数进入阻塞状态，直到有客户进程调用connect函数而建立起一个连接；
>5. 当与客户端创建连接后，服务器调用read_stream函数读取客户的请求；
>6. 处理完数据后，服务器调用write函数向客户端发送应答。
