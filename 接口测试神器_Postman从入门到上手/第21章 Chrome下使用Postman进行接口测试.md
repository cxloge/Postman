# 第21章 Chrome下使用Postman进行接口测试

[TOC]

　　在[**web**](javascript:;)和移动端开发时，常常会调用服务器端的接口进行数据请求，为了调试，一般会先用工具进行[**测试**](javascript:;)，通过测试后才开始在开发中使用。

## 工具：

　　　　（1）chrome浏览器

　　　　（2）[**postman**](javascript:;)（一种网页调试与发送网页http请求的chrome插件）

　　　　可以很方便的模拟请求来调试接口，常见的有：get、post、put、delete

### 1、Postman的安装（比较简单，此处不再描述）

### **2、进入Postman**

　　　　1）打开Chrome，依次选择选项>>更多工具>>扩展程序，选择Postman，点启动

　　　　2）在地址栏里直接输入：chrome://extensions/ ，点启动

[![img](http://www.51testing.com/attachments/2017/09/15201284_201709261440551l9RT.png)](http://www.51testing.com/batch.download.php?aid=75134)

　　　　Postman的进入方式.png

　　　　3）在地址栏里直接输入：chrome://apps/，点击Postman图标进入

[![img](http://www.51testing.com/attachments/2017/09/15201284_2017092614413913fo6.png)](http://www.51testing.com/batch.download.php?aid=75136)

　　　　Postman的进入方式.png

　　　　4）点击桌面应用

　　　　**启动后的页面**

[![img](http://www.51testing.com/attachments/2017/09/15201284_2017092614420016On6.png)](http://www.51testing.com/batch.download.php?aid=75137)

　　　　启动后页面展示.png

　　　　默认的postman会自带一个demo的项目（POSTMAN Echo），里面有各种场景的用例demo

　　　　比如 Request Methods 目录下面就有GET、POST、PUT、PATCH、DEL请求，，双击后右侧就会显示，点击【Send】可以查看响应结果。

　　　　初学者可以通过查看这些demo用例来学习如何使用这个工具，同时也可以修改 params 和 tests的内容来观察数据，从而加深理解。

## **下面开始利用Postman这个工具来模拟测试API 接口**

### 1、新建项目

　　　　点击【添加目录图标】来新增一个根目录（项目），可以把一个项目或一个模块的用例都存放在该目录下，另外还可以建立子目录来进行功能用例的细分，如下图所示：

[![img](http://www.51testing.com/attachments/2017/09/15201284_201709261442341XZze.png)](http://www.51testing.com/batch.download.php?aid=75138)

　　　　新建项目.png

[![img](http://www.51testing.com/attachments/2017/09/15201284_201709261442521nlKt.png)](http://www.51testing.com/batch.download.php?aid=75139)

　　　　建子目录和复制项目.png

### 2、新增用例及请求信息

　　　　接口文档-获取客户详情

[![img](http://www.51testing.com/attachments/2017/09/15201284_201709261443111b1Fa.png)](http://www.51testing.com/batch.download.php?aid=75141)

　　　　接口文档-获取客户详情.png

　　　　点击右侧区域的+号来新增一个空用例的模板，也可以通过复制一个已有用例来达到新建一个用例的目的，方法见下：

[![img](http://www.51testing.com/attachments/2017/09/15201284_201709261443251aRH4.png)](http://www.51testing.com/batch.download.php?aid=75142)

　　　　新建用例.png

　　　　**一般流程如下：**

　　　　1）选择一个请求方法，如：GET 或 POST

　　　　2）填写请求的url，如：http://demo.udesk.cn/open_api_v1

　　　　GET：则请求参数直接写在url后，用？连接（点击params，输入参数内容后会自动填充到URL中）

　　　　POST：请求添加在body中，而非url后

　　　　（若是以 json 格式提交数据，需要添加：Content-Type ：application/x-www-form-urlencoded，否则会导致请求失败）

　　　　如果需要发送带文件的请求时，就要改下请求格式了，具体如下：

[![img](http://www.51testing.com/attachments/2017/09/15201284_201709261443521fHos.png)](http://www.51testing.com/batch.download.php?aid=75143)

　　　　发送带文件的请求格式.png

　　　　3）点击“send”发送请求

　　　　4）查看请求响应内容

[![img](http://www.51testing.com/attachments/2017/09/15201284_2017092614441417lQq.png)](http://www.51testing.com/batch.download.php?aid=75144)

　　　　返回数据的格式.png

　　　　**技巧：**

　　　　如果误操作关闭了tab标签，可以到【History】中双击恢复

　　　　在收到response之后执行的测试，测试的结果会显示在【Tests】中

[![img](http://www.51testing.com/attachments/2017/09/15201284_201709261444461FP27.png)](http://www.51testing.com/batch.download.php?aid=75145)

　　　　测试结果

### 3、导出用例为代码

　　　　通过点击“Generate Code”一键生成代码，并且还有好多语言和类库可以选择

[![img](http://www.51testing.com/attachments/2017/09/15201284_201709261445061sltb.png)](http://www.51testing.com/batch.download.php?aid=75146)

　　　　导出用例为代码.png

### 4、设置环境

　　　　通过开发有自己的环境，测试也有专门的测试环境，另外还有生产环境，维护后以后只需直接切换即可

[![img](http://www.51testing.com/attachments/2017/09/15201284_201709261445211mApc.png)](http://www.51testing.com/batch.download.php?aid=75148)

　　　　设置环境.png

### 5、批量执行用例

　　　　该功能由单独的Runner来负责的，点击【Run】会弹出新界面，从而进行操作

[![img](http://www.51testing.com/attachments/2017/09/15201284_2017092614454411PFi.png)](http://www.51testing.com/batch.download.php?aid=75149)

　　　　批量执行用例

　　　　注意：请求支不支持post请求是由服务端决定。