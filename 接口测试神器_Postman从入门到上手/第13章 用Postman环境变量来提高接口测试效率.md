# 第13章 用Postman环境变量来提高接口测试效率

[TOC]

## Postman介绍

　　Postman是一款[**接口测试**](javascript:;)工具，在日常的接口开发中经常使用到。比如完成一个接口后，在提交给测试人员之前，开发人员要进行接口测试，这时候就要用到测试工具来提高测试效率，而 Postman 是测试工具中比较出众的一款。接口测试工具大同小异，开发人员都比较了解，所以下面的内容中主要介绍这款工具的使用技巧，了解这些会节省接口测试的时间，从而提高效率。

[![Postman 工具截图](http://www.51testing.com/attachments/2018/03/14982672_201803121028451ulFV.gif)](http://www.51testing.com/batch.download.php?aid=84035)　　

图一：Postman 工具截图

## 设置环境变量

　　设置环境变量的好处是：当接口服务更换域名时，只要把环境变量的域名地址更换就可以，不用浪费时间去修改每个接口地址。

　　大部分情况下，被测试的接口会有一些共同的信息，比如运行在同一台服务器上的接口可能拥有相同域名，同一个域名下的接口访问时需要带相同的认证信息。这里的同一个域名，我们可以认为是同一个环境（Environment），而域名地址和认证信息就可以作为环境变量。

　　接口服务开发完成后可能会在三个环境上部署，分别时开发环境、测试环境、生产环境，每个环境的域名或者 IP 是不同的，所以可以在 Postman 上建立三组环境变量来对应三个代码环境。

　　

[![增加环境变量](http://www.51testing.com/attachments/2018/03/14982672_201803121028452JKyf.gif)](http://www.51testing.com/batch.download.php?aid=84036)

图二：增加环境变量

　　如上图所示，为当前接口配置了三个环境，每个环境下的变量是相同的，使用环境变量的方法是双大括号嵌套变量名，如“{{doman}}”。但是上图中的接口访问并没有成功，原因是没有带入认证信息 token 。token 是从登录接口获取的，如果能把登录接口返回的 token 直接赋值给环境变量 token，这样其他需要认证的接口就可以直接从环境变量读取 token，该如何实现？

## 自动修改环境变量的值

　[![img](http://www.51testing.com/attachments/2018/03/14982672_201803121028453mWto.gif)](http://www.51testing.com/batch.download.php?aid=84037)　

图三：自动修改环境变量 token

　　如上图，登录接口访问成功后，环境变量的 token 被成功赋值，其他接口可以这样配置，就可认证成功：

　[![img](http://www.51testing.com/attachments/2018/03/14982672_20180312102845430Bk.png)](http://www.51testing.com/batch.download.php?aid=84038)　

图四：配置使用认证信息

　　把下面的代码粘贴到 Tests 中，代码会在当前接口访问结束后执行，给环境变量 token 赋值：

　　// 解析接口返回的 json 数据

　　var jsonData = JSON.parse(responseBody);

　　// 将返回结果中的 bizContent.token 赋值给 环境变量 token

　　postman.setEnvironmentVariable("token", jsonData.bizContent.token);

　　[![img](http://www.51testing.com/attachments/2018/03/14982672_201803121028455CmBH.png)](http://www.51testing.com/batch.download.php?aid=84039)

图五：修改环境变量的代码