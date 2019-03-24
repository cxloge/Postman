# 第05章 Postman接口测试系列：基本操作总结

[TOC]

　　最近项目需要[**接口测试**](javascript:;)，所以选择了不少工具对比，最终决定使用[**postman**](javascript:;)进行接口测试，这个工具目前使用比较简单，但是有点还是比较多的，如下：

　　1、方便切换不同的环境进行接口测试工作，而不用修改变量或代码

　　2、可以在[**浏览器**](javascript:;)中直接只用插件(目前[**谷歌**](javascript:;)系统插件已经不更新了)

　　3、可以和newman和jenkins集成进行自动化构建，比较方便

## 安装

### 安装方法一：插件安装

　　直接通过chrome插件进行安装，简单快捷（推荐此方法），前提是必须FQ，这里推荐使用谷歌访问助手进行FQ，下载postman插件进行安装。

　　谷歌访问助手下载地址：见[**百度**](javascript:;)网盘地址：链接: https://pan.baidu.com/s/1o8eJiSM 密码: hek2，将使用的谷歌插件和postman插件下载至本地之后，安装谷歌插件和postman插件。

　　插件安装说明直接将插件拖至谷歌浏览器的扩展程序中即可完成安装，如图

[![img](http://www.51testing.com/attachments/2017/12/14982672_20171204152952160cN.jpg)](http://www.51testing.com/batch.download.php?aid=78543)

　　安装完成之后，在谷歌中打开新的标签页，点击应用，如图

[![img](http://www.51testing.com/attachments/2017/12/14982672_201712041529528Wy0S.jpg)](http://www.51testing.com/batch.download.php?aid=78550)

　　在打开的应用页面中，点击postman即可打开应用，如图

[![img](http://www.51testing.com/attachments/2017/12/14982672_201712041529529BeSh.jpg)](http://www.51testing.com/batch.download.php?aid=78551)

### 安装方法二：下载的exe文件直接安装

## 使用

### Postman界面介绍

[![img](http://www.51testing.com/attachments/2017/12/14982672_2017120415295210DOGI.jpg)](http://www.51testing.com/batch.download.php?aid=78552)

　　接下来，简单介绍下每个功能区都能做些什么事：

　　快捷区： 快捷区提供常用的操作入口，包括运行收藏夹的一组测试数据，导入收藏夹测试数据，或环境配置数据。

　　设置区： 软件的常用设置（主题设置、快捷键设置等），以及导出环境数据。

　　侧边栏： 主要是 Request 请求的历史[**记录**](javascript:;)，和收藏夹管理。

　　搜索栏： 输入关键字，可以搜索 Request 历史、收藏夹、收藏夹内的请求。

　　功能区： Request 请求设置，查看 Response 响应结果和测试结果。

　　参考 http://blog.csdn.net/water_0815/article/details/53263643

### Postman功能

　　· 主要用于模拟网络请求包

　　· 快速创建请求

　　· 回放、管理请求

　　· 快速设置网络代理

　　https://www.getpostman.com/features

### Post请求：

　　这里我们先看一下接口的需求文档，如图

   [![img](http://www.51testing.com/attachments/2017/12/14982672_2017120415295211DHfa.jpg)](http://www.51testing.com/batch.download.php?aid=78553)

　　页面访问请求 http://192.168.1.6/Api/request/createSession

　　1、在地址栏中输入请求的url：http://192.168.1.6/Api/request/createSession

　　2、选择请求方式:post请求

　　3、点击”application/x-www-form-urlencoded”,

　　4、添加key和value信息，如图

[![img](http://www.51testing.com/attachments/2017/12/14982672_2017120415295212O46C.jpg)](http://www.51testing.com/batch.download.php?aid=78554)

### 环境设置

　　postman中可以设置多种不同环境，方便collections切换在不同的环境中运行而不用再次修改接口信息，如图：

[![img](http://www.51testing.com/attachments/2017/12/14982672_2017120415295213x8JO.jpg)](http://www.51testing.com/batch.download.php?aid=78555)

　　图中显示的客户环境和测试环境就是配置的2种环境信息；

### 环境的设置操作

　　在上图显示的界面中，点击” 设置”按钮--manage environments，打开环境设置界面，如图所示

[![img](http://www.51testing.com/attachments/2017/12/14982672_2017120415295214B8tU.png)](http://www.51testing.com/batch.download.php?aid=78556)

　　在环境界面中添加环境信息，之后点击Add即可完成环境的配置。

　　环境中存在两种变量，一种是环境变量，相当于局部变量；另外一种是全局变量(globals)。

## 环境变量：

　　当使用API的时候，你可能经常需要使用不同的设置。环境设置可以让你使用变量自定义request。这个方法可以让你轻松的在不同的设置之间改变而不用改变你的request。你不需要担心要记住Postman中所有的这些变量的值。环境可以下载保存为JSON文件，以后可以再加载他。

　　参考http://www.jianshu.com/p/bffbc79b43f6

### 1、环境变量的设置

　　第一种方法：在具体的环境中，设置该环境的key和value值，如图

[![img](http://www.51testing.com/attachments/2017/12/14982672_20171204152952150zIJ.jpg)](http://www.51testing.com/batch.download.php?aid=78557)

　　第二种方法：直接在代码中设置变量

　　可以在postman主页面中的pre-request Script中设置环境变量

　　设置环境变量：

　　postman. setEnvironmentVariable (“key”, “value”);

　　environment.key= " value ";

　　环境变量可以使用在以下地方：

　　· URL

　　· URL params

　　· Header values

　　· form-data/url-encoded values

　　· Raw body content

　　· Helper fields

　　在你要使用的变量名上附上双花括号。

## 全局变量：

　　全局变量提供了一组总是有效的变量。你可以有很多环境变量，但是同一时间只能有一组有效。但是你可以像使用环境变量一样使用全局变量。

### 1、全局变量设置

　　和环境变量一样，第一种可以在环境设置中添加全局变量，如图

[![img](http://www.51testing.com/attachments/2017/12/14982672_201712041529522Dsnn.png)](http://www.51testing.com/batch.download.php?aid=78544)

　　点击globals按钮，打开全局变量添加页面，参考环境变量设置进行操作。

　　第二种方法：

　　可以在postman主页面中的pre-request Script中设置全局变量

　　设置全局变量：

　　postman. setGlobalVariable (“key”, “value”);

### 说明

　　当全局变量和环境变量出现同样的key时，环境变量会覆盖全局变量的key值

### 读取变量

　　在接口信息中，可以使用{{key}}来获取变量信息，如图

[![img](http://www.51testing.com/attachments/2017/12/14982672_2017120415295238pzx.png)](http://www.51testing.com/batch.download.php?aid=78545)

　　pre-request Script读取变量：

　　getEnvironmentVariable ("key");//获取key的环境变量

　　getGlobalVariable(“key”);//获取key的全局变量

## 断言(部分)

### collections

　　可以将编写的接口用例加入collections，便于执行runner操作；加入界面如图

[![img](http://www.51testing.com/attachments/2017/12/14982672_2017120415295242ude.png)](http://www.51testing.com/batch.download.php?aid=78546)

### Runner

　　在postman主页面中，点击runner，打开运行界面，

[![img](http://www.51testing.com/attachments/2017/12/14982672_201712041529525nhIL.png)](http://www.51testing.com/batch.download.php?aid=78547)

　　在runner页面中，左侧显示的是历史运行结果，中间是需要进行测试的接口用例信息，其中Environment显示的是需要进行的环境设置，而Iteration是需要进行迭代的次数；而右侧显示的是运行接口用例详情。

## 其他操作

　　1、接口用例在浏览器中展示操作

　　在postman界面中，点击” 向左的箭头 ”按钮，右侧显示的界面中，view in web操作可以在浏览器中展示接口用例信息；run可以运行需要进行测试的接口用例信息；

　　导出操作

　　2、在postman界面中，点击“...” 打开的页面中，

　　Edit可以编辑Collections的描述信息；

　　Rename重命名collections

　　Add Folder添加文件夹

　　Duplicate 复制collections

　　Export 导出collections

　　如图所示

[![img](http://www.51testing.com/attachments/2017/12/14982672_201712041529526rqFV.png)](http://www.51testing.com/batch.download.php?aid=78548)

　　以上就是postman接口测试基本使用方法总结，接口测试用例的基本测试点如图所示

[![img](http://www.51testing.com/attachments/2017/12/14982672_201712041529527DGjX.png)](http://www.51testing.com/batch.download.php?aid=78549)

相关推荐：

[Postman接口测试系列：时间戳和加密](http://www.51testing.com/html/30/n-3722830.html)

[Postman接口测试系列：接口参数化和参数的传递](http://www.51testing.com/html/31/n-3722831.html)