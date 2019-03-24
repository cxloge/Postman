# 第04章 Postman设置环境变量

[TOC]

## 问题描述：

设置环境变量，变化接口访问的地址，例如localhost，换成其他IP地址。

　　例如：有个接口login

　　本地访问为：http://localhost:8061/login

　　[**测试**](javascript:;)环境为：http://11.11.11.136:8061/login

　　可以把IP地址根据环境动态的改变，就需要Postman中的环境变量来解决。

## 解决思路：

　　1：在Postman中设置两个环境，本地环境、测试环境

　　2：在两个环境中分别设置变量名为 base_url的变量，存放各自环境的IP地址

　　Postman 中获取环境变量值的方式为：{{变量名}}，这样就可以获取变量值。

　　这里base_url的值获取方式就是： {{base_url}}

　　3：在Postman的URL地址栏中设置 为 {{base_url}}/login

　　4：切换不同的环境，base_url的值就会发生改变，这样就达到了IP地址切换的效果。

## 设置环境变量：

### 第一步：图右上角配置按钮

[![img](http://www.51testing.com/attachments/2018/03/14982672_201803061417241EpY6.png)](http://www.51testing.com/batch.download.php?aid=83732)

　　点Manage Environmens, 如下图

[![img](http://www.51testing.com/attachments/2018/03/14982672_201803061417242Cbb1.png)](http://www.51testing.com/batch.download.php?aid=83733)

　　我已经设置了两个环境，下面我们设置第三个环境，

### 第二步：137环境变量

　　点击Add按钮，如下图所示结果

[![img](http://www.51testing.com/attachments/2018/03/14982672_201803061417243FTUV.png)](http://www.51testing.com/batch.download.php?aid=83734)

　　点击Add添加成功，这里要说明的是上面的136环境，和本地测试环境也都有这个base_url变量，只是值不同，就是切换这个环境取不同的base_url值达到环境的切换。

　　如下图所示，环境变量添加完毕

[![img](http://www.51testing.com/attachments/2018/03/14982672_201803061417244O0S9.png)](http://www.51testing.com/batch.download.php?aid=83735)

　　现在有了三个环境，演示一下怎么切换，效果如何。

### 第三步：环境切换演示

[![img](http://www.51testing.com/attachments/2018/03/14982672_201803061417245t3kC.png)](http://www.51testing.com/batch.download.php?aid=83736)