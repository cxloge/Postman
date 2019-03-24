# 第09章 使用jenkins优化自动化执行方式

[TOC]

## 背景

　　最近组内在优化之前的自动化执行框架，目的是解决之前自动化存在的问题； 

　　由此引入了jenkins去构建自动化用例的执行；

## 期望状态

　　自动化框架和case维护在svn；

　　由于case是按模块划分，而目前每个模块可能由不同的[**测试**](javascript:;)人员负责，所以期望模块的执行结果邮件发给对应的测试负责人；

　　由于不同模块关注点不同，需要的系统环境也不同，所以需要使用不同执行机执行；

　　期望对待上线版本，一键部署自动化执行；

　　期望每天夜间执行全部用例，以发现当天新增的严重问题；

## 实现方案

　　通过jenkins的svn插件实现任务环境准备时更新最新框架及用例；

　　通过优化自动化框架（python unittest）执行参数，支持不同参数执行不同用例；

　　jenkins创建多个任务，每个任务使用不同机器执行；

　　写一个接口，接口实现远程调用jenkins命令行方式启动任务；

　　jenkins crontab任务实现定时执行；

## 实现流程

[![img](http://www.51testing.com/attachments/2017/09/15201284_201709211548381JRm7.jpg)](http://www.51testing.com/batch.download.php?aid=74901)

　　实际配置

　　●任务名

[![img](http://www.51testing.com/attachments/2017/09/15201284_201709211548551Glvu.jpg)](http://www.51testing.com/batch.download.php?aid=74902)

　　●基本配置

[![img](http://www.51testing.com/attachments/2017/09/15201284_201709211549111I4VR.jpg)](http://www.51testing.com/batch.download.php?aid=74903)

　　●svn配置

[![img](http://www.51testing.com/attachments/2017/09/15201284_201709211549241lgzP.jpg)](http://www.51testing.com/batch.download.php?aid=74904)

　　●构建配置

[![img](http://www.51testing.com/attachments/2017/09/15201284_201709211549421DjTc.jpg)](http://www.51testing.com/batch.download.php?aid=74905)

　　●远程调用命令行

　　●[**java**](javascript:;) -jar /search/odin/jenkins/jenkins-cli.jar -s http://10.10.10.10:8080/ build SE_Auto_XXXX -p version=".$version; 通过jenkins提供的命令行jar包： 

　　第一个参数：jenkins服务地址； 

　　第二个参数：执行什么动作（这里填build，就是立即构建）； 

　　第三个参数：执行哪个任务； 

　　-p：任务所需要的参数名（version），这里使用接口调用方传来的实际版本号；

　　●crontab配置

[![img](http://www.51testing.com/attachments/2017/09/15201284_201709211550041QCq9.jpg)](http://www.51testing.com/batch.download.php?aid=74906)

　　以上就是利用jenkins配合自动化框架优化构建方式的简单例子，jenkins还有很多功能待发掘，你知道什么好用的插件或者nb的使用方法吗？闷声不能发大财，回复过来，我们也好提高自己的姿势水平。