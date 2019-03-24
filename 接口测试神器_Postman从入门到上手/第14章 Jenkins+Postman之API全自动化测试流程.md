# 第14章 Jenkins+Postman之API全自动化测试流程

[TOC]

## 1、背景

　　本文要介绍的环境在我司已经投入使用，举个简单的真实使用场景，开发提供了300多个API，每个API都有各种参数，所以我们会先在[**postman**](javascript:;)中为这300多个API编写300*n个testcase，然后在[**jenkins**](javascript:;)上跑；到此有人可能会问，都在postman中写好testcase了，怎么还要去jenkins中跑，岂不是多此一举？答案是否定的，试想，当开发一直在不停的维护这300多个接口时，难道需要开发每次都告诉我们[**测试**](javascript:;)人员该进行测试了吗？显然不是的，这就是jenkins+postman的自动化之处了，开发可以实现一个jenkins的上游job脚本（当接口代码有修改时触发我们这个testcase的下游job），当他们每次修改维护接口时不需要进行任何操作与交流，代码一旦提交jenkins就能自动化个性化地开始执行我们预定于的那些testcase了，然后我们只用关注最终的测试结果邮件即可，这样大大的提高了开发测试效率。

　　鉴于国内很少测试工程师用postman来测试API，于是写本篇[**文章**](javascript:;)分享下。前一个月用postman写了API自动化测试脚本，并用newman命令行运行所有测试案例，觉得没有达到全[**自动化测试**](javascript:;)，于是配置jenkins job来运行API自动化测试脚本，使API达到完全自动化测试！

## 2、环境配置与运行

　　这部分依次展示了如何安装设置及运行一个基于Postman的自动化工具，具体如下。

### **2.1、postman 安装**

　　在[**谷歌**](javascript:;)[**浏览器**](javascript:;)下载postman插件，并安装，下载路径（Chrome应用商店需要翻墙）：https://chrome.google.com/webstore/search/postmanhl=en。这个比较小儿科，一句话带过就行了。（不过要注意，建议最好下载应用，而不是插件，因为功能强大一些）。

### 2.2、newman 的安装

　　第一步，安装nodejs。

　　第二步，在nodejs命令行安装newman，即命令行输入如下命令：

　　npminstall-g newman

　[![img](http://www.51testing.com/attachments/2018/03/14982672_201803071451431FOoY.png)](http://www.51testing.com/batch.download.php?aid=83844)

### 2.3、jenkins 安装

　　去官网（https://jenkins.io/index.html）下载jenkins，各种下一步点击安即可（官网wiki等目录下一般都有不同平台的安装文档，依据文档安装即可）。

### 2.4、postman 使用与导出

　　第一步，创建一个放置testCase的文件夹Test，如下：

[![img](http://www.51testing.com/attachments/2018/03/14982672_201803071451432nbSf.png)](http://www.51testing.com/batch.download.php?aid=83845)

　　第二步，创建第一个testcase，点击下图1处的加号新增一个case，在2处选择你的API请求方式，在3处写上api请求的url，在4处填写该请求的相关参数，具体如下图：

[![img](http://www.51testing.com/attachments/2018/03/14982672_201803071451433bjjn.png)](http://www.51testing.com/batch.download.php?aid=83846)

　　下面展示了一个依据上图步骤配置后的邮箱地址请求示例，如图：

[![img](http://www.51testing.com/attachments/2018/03/14982672_201803071451434M1qy.png)](http://www.51testing.com/batch.download.php?aid=83847)

　　第三步，对一个testCase的判断可以写在如下所示位置（判断的意思是指譬如返回的状态码、内容等是不是你期望的值）：

[![img](http://www.51testing.com/attachments/2018/03/14982672_201803071451435jtSt.png)](http://www.51testing.com/batch.download.php?aid=83848)

　　第四步，点击send按钮即可发送一个请求，同时可以看到请求的结果，如图：

[![img](http://www.51testing.com/attachments/2018/03/14982672_201803071451436VroC.png)](http://www.51testing.com/batch.download.php?aid=83849)

　　当然，一般Test目录可能有很多的testCase，这种情况下我们可以选中文件夹，然后点击start Test按钮，这样就会自动执行文件夹内的所有testcase并显示测试结果，如图：

[![img](http://www.51testing.com/attachments/2018/03/14982672_201803071451437p9Rb.png)](http://www.51testing.com/batch.download.php?aid=83850)

　　第五步，导出上面在postman中写的testCase文件和设置的环境变量文件（如下图导出testCase alarm detail 文件 和 environment 文件）。这是最重要最核心的一步，自动化的源头依赖于此步，请务必注意。

[![img](http://www.51testing.com/attachments/2018/03/14982672_201803071451438tilj.png)](http://www.51testing.com/batch.download.php?aid=83851)

[![img](http://www.51testing.com/attachments/2018/03/14982672_201803071455051h78o.png)](http://www.51testing.com/batch.download.php?aid=83853)

　　至此postman的基本使用和导出就完事了，关于postman的其他主题设置、登录等等其他功能请自行摸索，其实很多开发也非常喜欢用postman，譬如移动端开发喜欢用postman去请求服务端提供的API，以此来简单快捷验证接口的正确性和Json、xml等数据格式。

### 2.5、jenkins 配置

　　在jenkins上配置如下图，这个路径就是上面通过postman导出文件的路径。

[![img](http://www.51testing.com/attachments/2018/03/14982672_201803071451439VlhN.png)](http://www.51testing.com/batch.download.php?aid=83852)

　　剩下的就是jenkins的常规操作了，譬如设置好邮箱后点击立即构建或者设置多久构建一次，这样自动化就跑起来了，等待自动化测试结束后我们就可以收到测试成功或者失败的测试报告邮件（依赖于你的设置）了。

　　通过上面这些步骤即可完成基于postman和Jenkins的自动化[**接口测试**](javascript:;)。

## 3、总结

　　可以看见，其实postman就是一个GUI的工具，我们完全可以手动用它验证接口，但是当有海量接口且有序执行时就比较麻烦了，所以我们可以通过postman将所有接口的测试案例进行编写实现及导出；而由于postman导出的文件想在jenkins上通过命令行执行依赖于newman环境，所以我们安装配置了newman，以此就能解决jenkins只能执行命令行或者脚本的弊端；他们几个的结合就实现了一次测试案例的编写实现个性化自动化的接口测试。