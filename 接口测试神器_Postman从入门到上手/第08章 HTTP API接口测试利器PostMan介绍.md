# 第08章 HTTP API接口测试利器PostMan介绍

[TOC]

## 一、什么是API接口测试？

　　API接口有多种，个人将其划分为三类。

　　第一种是函数级别的，测试需要对接口的各个参数进行测试，如：

　　Int getResult（String key， String ID， Int ticket）。

　　第二种是对象级别的，开发在使用API接口时，先引入包名，在使用之前声明一个对象，之后可以使用对象提供的方法，而测试时，需要测试的是API的功能及对数据输入的正确性。第二种和第一种的差别是，我们只需关注提供给用户使用的接口就可以了，不用关心接口调用其他函数情况，相对于第一种来说，测试的粒度要大一些，范围小一些。

　　第三种是http协议的接口，App客户端和后端服务连接，一般采用的都是http协议，客户端通过get和post的方法从后端服务获取数据。第三种相对于第二种来说，粒度更大，我们关注的接口更少，但是这些接口都是核心功能。

## 二、为什么要测试API接口？

　　App后端服务，在出现功能异常时，或者吐出异常数据时，可能会导致客户端功能异常，甚至出现崩溃的现象。而客户端由于数据的问题而崩溃，如果容错不到位，可能导致App永远无法启动。这种伤害，对用户，对公司来说，都是巨大的。因此有必要进行API接口的测试。

## 三、如何来测试API接口？

　　目前测试API接口的方法很多，如：使用fiddler的发送get、post的功能进行校验。缺点是，测试一遍后，在回归测试时，需要手动再执行一遍，非常耗时。

　　有人建议使用python的request进行API接口测试时，通过编码方式进行API接口测试，的确是一个好的方法。但是问题是，时间。在有限的测试时间内，可能没有时间去做这个脚本。如果完成这个脚本，至少要进行一轮手工测试，从而才能了解到期望的返回值是什么样的。

　　有没有这样一种工具，手动测试完成后，不需要写太多代码，立马可以用功能性测试的cases进行自动化回归呢？

　　答案：有。[**PostMan**](javascript:;)就是这一款工具，既可以像使用Fiddler一样，也可以像使用脚本一样。

　　o试用范围：http  API接口的测试

　　o支持的平台：windows & Mac OS

## 1.环境的搭建

　　1)安装chrome浏览器

　　2)在chrome地址栏打开： https://chrome.google.com/webstore/search/postman

　　3)填加postman 和 postman interceptor

　　opostman是一个独立的chrome app；

　　opostman interceptor 可以和postman进行数据同步，并将chrome浏览器中的浏览[**记录**](javascript:;)发送到postman。

　　4)在chrome地址栏打开： chrome://extensions/

　　点击postman下的"详细信息"，填加快捷方式到桌面。

　　5)启动postman并注册一个账号。

## 2.Postman的使用

　　1)在chrome浏览器中打开postman interceptor同步开关

[![img](http://www.51testing.com/attachments/2016/07/14982672_2016071916295616qH7.jpg)](http://www.51testing.com/batch.download.php?aid=61252)

　　2)启动post man，打开同步开关

[![img](http://www.51testing.com/attachments/2016/07/14982672_201607191629565r0Kn.jpg)](http://www.51testing.com/batch.download.php?aid=61256)

　　3)在chrome浏览器中访问搜狗首页，在postman history的tab下可以看到访问的记录

[![img](http://www.51testing.com/attachments/2016/07/14982672_201607191629566qxce.jpg)](http://www.51testing.com/batch.download.php?aid=61257)

　　4)填加一个检查点

[![img](http://www.51testing.com/attachments/2016/07/14982672_201607191629567eSk2.jpg)](http://www.51testing.com/batch.download.php?aid=61258)

　　o选择需要检查的请求，如：m.sogou.com, 点击 GET 请求右侧的 Send 按钮， 在body部分可以看到返回的数据。

[![img](http://www.51testing.com/attachments/2016/07/14982672_201607191629568pprf.jpg)](http://www.51testing.com/batch.download.php?aid=61259)

　　o点击请求部分底部的Tests，并从右侧检查点中，选择需要验证的点，如：验证返回的内容中包含"微信"，点击"Response body: Contains string"，则会在检验区域加入一行检查语句，并将要检查的字符串，改成"微信"。然后点击"Save"保存，将检查的请求添加到Collections中。

[![img](http://www.51testing.com/attachments/2016/07/14982672_201607191629569IdHj.jpg)](http://www.51testing.com/batch.download.php?aid=61260)

5)	自动运行检查的集合

　　o	点击"Collections"Tab，选择建立的集合，点击集合的"Run"按钮，进入Test页面。在Test页面选择，Start Test。

[![img](http://www.51testing.com/attachments/2016/07/14982672_20160719162956108Fu9.jpg)](http://www.51testing.com/batch.download.php?aid=61261)

　　6)	测试结果会在右侧的Results的tab中显示出来。

[![img](http://www.51testing.com/attachments/2016/07/14982672_2016071916295611shi0.jpg)](http://www.51testing.com/batch.download.php?aid=61262)

　　7)	PostMan支持多种不同的请求。从GET列表中可以选择需要测试的类型。

## 3.NewMan的使用

　　在正确性测试时，可以把要测试请求全部保存下来，这样可以在后续的bug验证及回归时使用。未来再有相同模块提测时，跑一遍之前的脚本，既可以完成之前功能的回归验证。

　　NewMan是命令行的工具，需要在PC上安装NPM，node环境。安装完成后，进行如下命令安装newman 。

[![img](http://www.51testing.com/attachments/2016/07/14982672_2016071916295612xn4g.jpg)](http://www.51testing.com/batch.download.php?aid=61263)

　　安装完成后，首先需要将postman中的脚本保存到本地，然后在命令行中执行，即可生成测试报告。

　　o	将PostMan的Collections保存到本地。

[![img](http://www.51testing.com/attachments/2016/07/14982672_2016071916295622yjN.jpg)](http://www.51testing.com/batch.download.php?aid=61253)

　　o	在命令行执行postman的脚本

　　o	newman -c Test.json.postman_collection -H result.html

[![img](http://www.51testing.com/attachments/2016/07/14982672_201607191629563s5pR.jpg)](http://www.51testing.com/batch.download.php?aid=61254)

　　o	运行完成后，会生成一个html结果页面。

[![img](http://www.51testing.com/attachments/2016/07/14982672_201607191629564XY3r.jpg)](http://www.51testing.com/batch.download.php?aid=61255)

## PostMan的优点是：

1.任何人都可以使用，不需要编码能力；

2.功能测试时的cases即刻可以变成自动化用例；

3.像使用Fiddler一样，查看数据的返回情况。
