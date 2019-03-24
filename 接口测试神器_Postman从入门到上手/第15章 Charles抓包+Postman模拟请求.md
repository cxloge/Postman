# 第15章 Charles抓包+Postman模拟请求

[TOC]

## 一、工具介绍

### 1.Charles(又称为青花瓷)

　　今天来介绍一下Mac上抓包工具Charles(又称为青花瓷)，官网可以下载，但是需要破解之后才能永久使用，当然，可以有30天试用期，具体的使用方法在此就不进行一一介绍了，如有需要再补上。（ps:[破解版下载地址](https://pan.baidu.com/s/1jk20aReX4Nb7JlftdOEtig)，密码:xkxa)。

　[![img](http://www.51testing.com/attachments/2018/03/14982672_201803061516081Fbdt.png)](http://www.51testing.com/batch.download.php?aid=83761)

### 2.Postman

　　[**Postman**](javascript:;)是一种网页调试与发送网页http请求的chrome插件。我们可以用来很方便的模拟get或者post或者其他方式的请求来调试接口。

[![img](http://www.51testing.com/attachments/2018/03/14982672_201803061516083VbZh.png)](http://www.51testing.com/batch.download.php?aid=83763)

## 二、开始抓取网络接口以及模拟请求

　　**第一步、**打开Charles,在[**浏览器**](javascript:;)中输入需要请求的地址，我这里访问的是一个投票的接口

　　显示信息如下：

　　[![img](http://www.51testing.com/attachments/2018/03/14982672_201803061516084COmC.png)](http://www.51testing.com/batch.download.php?aid=83764)

　　cookie信息：

　[![img](http://www.51testing.com/attachments/2018/03/14982672_201803061516085dIUG.png)](http://www.51testing.com/batch.download.php?aid=83765)

　　参数信息：

　[![img](http://www.51testing.com/attachments/2018/03/14982672_201803061516086p7XA.png)](http://www.51testing.com/batch.download.php?aid=83766)

　　**第二步、**在第一步获取了请求的url、cookie、参数等请求需要的之后我们就可以打开Postman来进行模拟请求了。

　[![img](http://www.51testing.com/attachments/2018/03/14982672_201803061516087HWX0.png)](http://www.51testing.com/batch.download.php?aid=83767)

　　配置信息如下：

　　[![img](http://www.51testing.com/attachments/2018/03/14982672_201803061516088bd7S.png)](http://www.51testing.com/batch.download.php?aid=83768)

　　body参数：

　　[![img](http://www.51testing.com/attachments/2018/03/14982672_201803061516089I3x5.png)](http://www.51testing.com/batch.download.php?aid=83769)

　　**第三步、**发送请求，看到后台返回的信息

　　[![img](http://www.51testing.com/attachments/2018/03/14982672_2018030615160810xvgu.png)](http://www.51testing.com/batch.download.php?aid=83770)

　　到这里这个请求接口的操作就模拟成功了，既然参数和地址都有了，这个时候就是你想做什么就做什么的时候了，你懂得。

　[![img](http://www.51testing.com/attachments/2018/03/14982672_201803061516082hLIA.png)](http://www.51testing.com/batch.download.php?aid=83762)

　　这是根据postman请求结果，自己随便写了个[**手机**](javascript:;)端来进行请求的，有兴趣的可以一起研究，欢迎骚扰。