# 第01章 Postman使用入门及实践思考

**起因**

　　由于很早就接触过 Postman，感觉确实挺好用的，因此在[**测试**](javascript:;)内部培训时，我准备了 Postman 工具的使用入门培训 PPT，经人提醒特此整理成文字形式。为了更好的说明，我适当补充了些文字。

[TOC]

## 1、概述

### 1.1 接口定义

　[![img](http://www.51testing.com/attachments/2018/03/14982672_201803011047281LeBG.png)](http://www.51testing.com/batch.download.php?aid=83495)　

接口

　　接口：这里特指软件接口，是指对协定进行定义的引用类型。通俗讲是就是软件系统不同组成部分衔接的约定。

　　通常就是所谓的API （Application Programming Interface） 应用程序编程接口，其表现的形式是源代码。

### 1.2、接口测试定义

　[![img](http://www.51testing.com/attachments/2018/03/14982672_20180301104728112lTe.png)](http://www.51testing.com/batch.download.php?aid=83505)　

测试金字塔

　　接口测试是测试系统组件间接口的一种测试。

　　接口测试主要用于检测外部系统与系统之间以及内部各个子系统之间的交互点。测试的重点是要检查数据的交换，传递和控制管理过程，以及系统间的相互逻辑依赖关系等。

　　——《[**百度**](javascript:;)百科》

### 1.3、Postman简介

　　[![img](http://www.51testing.com/attachments/2018/03/14982672_201803011047481G4vZ.png)](http://www.51testing.com/batch.download.php?aid=83513)

Postman主界面

　　Postman是由Postdot Technologies公司打造的一款功能强大的调试HTTP接口的工具，它最早是Chrome中最受欢迎的插件之一，现已扩展到Mac，[**Windows**](javascript:;)和[**Linux**](javascript:;)客户端。

　　软件功能非常强大，界面简洁明晰、操作方便快捷，设计得很人性化。

### 1.4、Postman主要特征

　　· 简单易用的图形用户界面；

　　· 保存API请求的历史[**记录**](javascript:;)；

　　· 无限制的使用集合、环境变量、运行测试和共享集合；

　　· 可用集合Runner来[**自动化测试**](javascript:;)；

　　· 灵活的API监控，运行时间、性能和准确；

　　· 模拟服务器，支持split-stack开发。

## 2、接口工具对比

### 2.1、指数对比

　[![img](http://www.51testing.com/attachments/2018/03/14982672_201803011047482rjs9.png)](http://www.51testing.com/batch.download.php?aid=83514)　

百度搜索指数

　　可以看到近1年里，大家对于Postman的关注度一直很高，最近几个月的涨幅更高了。

　　题外话：十一放假，都出去玩儿了，没人用百度了。

### 2.2、竞品对比

　[![img](http://www.51testing.com/attachments/2018/03/14982672_201803011047483CXs8.png)](http://www.51testing.com/batch.download.php?aid=83515)　

竞品对比

　　Postman在同类竞品中，并不是那么全面的，但为什么还有辣么多人用呢？我们往下看。

### 2.3、Postman具体优势

　　总结的几点参考优势。

　　简洁性：软件界面设计简洁有设计感；

　　易用性：容易上手，查看官方文档或搜搜博客，可以很快地掌握其用法；

　　实用性：可以快速进行开发调试，并展示响应结果， URL 创建简单，且方便查看与管理；

　　同步性：同步并备份账号数据（集合、文件夹、要求、回应、标题预设、环境、环境变量、全局变量、收集运行结果）。

## 3、Postman入门

### 3.1、安装

[![img](http://www.51testing.com/attachments/2018/03/14982672_201803011047484XDpP.png)](http://www.51testing.com/batch.download.php?aid=83516)　　

安装1

　　1. Postman：

　　可用作Mac，Windows和Linux操作系统的本地应用程序。

　　要安装Postman，请转至官网，然后单击下载适用于Mac / Windows / Linux的客户端。

　　安装过程没有特别需要说明的，具体安装步骤不赘述，详情查看官网。

　[![img](http://www.51testing.com/attachments/2018/03/14982672_2018030110474857G5W.png)](http://www.51testing.com/batch.download.php?aid=83517)　

安装2

　　2. Postman Chrome插件：

　　目前推荐客户端，由于Chrome插件已被弃用，但插件还可以继续运行，且只能在Chrome浏览器上运行。

### 3.2、界面设计

　　[![img](http://www.51testing.com/attachments/2018/03/14982672_201803011047486rwJA.png)](http://www.51testing.com/batch.download.php?aid=83518)

主界面UI

　　Header toolbar 标题栏即顶部工具栏，包含主要功能。

　　Sidebar 侧边栏可以查找、管理请求和集合。侧边栏分两个主要选项卡： History（历史记录）和 Collections（集合）。

　　Builder 构建器，在构建器中发送和管理API请求。上半部分是请求构建器，下半部分是响应查看器。

　　Status bar 状态栏在底部，提供了部分功能的快捷方式。

　[![img](http://www.51testing.com/attachments/2018/03/14982672_201803011047487BfCF.png)](http://www.51testing.com/batch.download.php?aid=83519)　

实际主界面

　　想了解更多可以查看Postman官方文档。

### 3.3、How to work

　[![img](http://www.51testing.com/attachments/2018/03/14982672_201803011047282itNO.png)](http://www.51testing.com/batch.download.php?aid=83496)　

官网示意图

　　在Postman中输入您的请求详细信息（URL :），注意请求方法【get】，然后点击发送【发送】按钮；

　[![img](http://www.51testing.com/attachments/2018/03/14982672_201803011050571ZJg9.png)](http://www.51testing.com/batch.download.php?aid=83520)

输入URL地址

　　该请求由API服务器接收，并且它返回一个响应；

　　Postman收到回复，并在界面中显示回复。

[![img](http://www.51testing.com/attachments/2018/03/14982672_201803011047283DLJZ.png)](http://www.51testing.com/batch.download.php?aid=83497)　　

显示回复

　　注：

　　上图接口是Postman的示例接口，参数就带在地址的后面以‘？’连接，响应结果可切换显示方式。

　　点击上图【JSON】可以选择其他显示模式。

## 4、实践思考

### 4.1、接口项目实践思路

　　1、测试接口文档

　　检验接口文档的完整性、正确性、一致性、易理解性和易浏览性。

　　这个一般在实际测试过程中，都会弱化测试，不注重。

　　2、编写[**测试用例**](javascript:;)

　　这个大家都熟，根据接口文档编写测试用例。用例编写方法可以按照[**黑盒测试**](javascript:;)的用例编写规则来编写，如：边界值、正交表等等设计方法。

　　3、执行测试并出报告

　　根据用例执行测试，注意验证预期结果，执行结束后出具测试报告。

　　4、持续集成测试

　　搭建持续集成自动化测试框架。

### 4.2、接口文档

　　内部培训时用的是公司内部的文档，现在只能换开放API。

　　接口文档某个接口一般包括：

　　· 接口功能

　　· 请求方式

　　· 入参

　　· 出参

　　· 示例

　　如图：

　[![img](http://www.51testing.com/attachments/2018/03/14982672_201803011047284gxlv.png)](http://www.51testing.com/batch.download.php?aid=83498)　

豆瓣搜索图书接口

　　此豆瓣开发者API链接：https://developers.douban.com/wiki/?title=book_v2#get_book

4.2.1 步骤1

　　使用Postman工具发送该Get请求，依据3.3节操作，如图：

　　[![img](http://www.51testing.com/attachments/2018/03/14982672_201803011047287jvVz.png)](http://www.51testing.com/batch.download.php?aid=83501)

搜索软件测试

**4.2.2 步骤2**

　　添加测试代码：

　　status code等于200

　　Response body中包含字符串“软件测试”

　　注：测试代码可以依情况自己加，所以我加了。

[![img](http://www.51testing.com/attachments/2018/03/14982672_201803011047288whmu.png)](http://www.51testing.com/batch.download.php?aid=83502)

　　测试断言

　　这里我另加了测试“响应时间小于200ms”，看到响应超过了200ms，是720ms。

　　再注：Postman有很多实例可以查看

　　[![img](http://www.51testing.com/attachments/2018/03/14982672_201803011047289QzlL.png)](http://www.51testing.com/batch.download.php?aid=83503)

实例

### 4.3、集成测试

　　主要是利用postman出的插件Newman：

　[![img](http://www.51testing.com/attachments/2018/03/14982672_2018030110472810wOHu.png)](http://www.51testing.com/batch.download.php?aid=83504)

Newman

　　上图为官网截图，介绍的主要意思就是借助Newman，可以将Postman集合与构建系统集成在一起。而我们用的比较多的构建就是Jenkins。Newman是一个命令行集合运行工具。

　　下图为集成测试示意图：

　[![img](http://www.51testing.com/attachments/2018/03/14982672_2018030110472812OQV1.png)](http://www.51testing.com/batch.download.php?aid=83506)　

集成测试

4.3.1 步骤1

　　搭建环境：

　　安装Node.js（Newman基于Node.js），安装Newman （参阅Newman官网），安装Jenkins（自行搜索安装过程）。

4.3.2 步骤2

　　导出集合：

　　先保存

　[![img](http://www.51testing.com/attachments/2018/03/14982672_2018030110472813lM7g.png)](http://www.51testing.com/batch.download.php?aid=83507)　

保存接口

　　再导出

　[![img](http://www.51testing.com/attachments/2018/03/14982672_20180301104728153mhZ.png)](http://www.51testing.com/batch.download.php?aid=83509)

导出1

　[![img](http://www.51testing.com/attachments/2018/03/14982672_2018030110472816gLmy.png)](http://www.51testing.com/batch.download.php?aid=83510)

导出2

　　我导出保存到了桌面，是一个json集合。

4.3.3 步骤3

　　通过Jenkins 构建时调用Newman，来执行接口测试。

　　构建的命令：

　　C:\Users\yawa1hz1\AppData\Roaming\npm\newman -c C:\Users\yawa1hz1\Desktop\test.postman_collection.json

　　[![img](http://www.51testing.com/attachments/2018/03/14982672_2018030110472817XTGq.png)](http://www.51testing.com/batch.download.php?aid=83511)

构建命令

　　选择构建的方式Execute Windows batch command，即批处理命令。新建Jenkins项目选自由项目，其他除必填项，都可以不管。

　　注：这段命令直接运行与window的cmd也是可以的。详细Newman命令参见官网。

　　新建任务完成后，执行构建

　[![img](http://www.51testing.com/attachments/2018/03/14982672_20180301104728184DGk.png)](http://www.51testing.com/batch.download.php?aid=83512)　

构建

　　可在 [Console Output]查看，但由于网页编码格式不同，显示乱码，可点击[View as plain text]查看，如图

　[![img](http://www.51testing.com/attachments/2018/03/14982672_201803011057431Edeb.png)](http://www.51testing.com/batch.download.php?aid=83522)　

构建结果乱码

　　可以看到构建失败（由于某个断言failed），和乱码（网页编码格式不同）。

　[![img](http://www.51testing.com/attachments/2018/03/14982672_201803011057561ORWL.png)](http://www.51testing.com/batch.download.php?aid=83523)　

结果查看

　　可以看到，我新加的“响应时间小于200ms”测试没通过，所以构建失败了。看官可以试试更改“响应时间小于1000ms”，应该就可以构建成功，断言无failed了。

## 5、总结

　　Postman还有很多功能，像 Runner 功能，目前只是介绍了基础使用，更多操作可以阅读官方文档。还有一点需要提一下，Postman 还是比较适合功能测试和开发调试 API 时使用。当然，Postman 也有 Pro 版（当然是要钱的，也可以试用看看）。

[TOC]