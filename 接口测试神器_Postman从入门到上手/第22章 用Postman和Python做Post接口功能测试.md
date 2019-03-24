# 第22章 用Postman和Python做Post接口功能测试

　前几天，在做一个post请求的接口[**功能测试**](javascript:;)的时候，发现数据始终无法入库，

　　认真加仔细检查了请求的url、方式、参数，均没有问题。

[![img](http://www.51testing.com/attachments/2017/08/15201284_201708071502311LHTt.png)](http://www.51testing.com/batch.download.php?aid=72176)

　　找到[**技术**](javascript:;)确认，原来是需要传json格式数据

　　在头信息中加上类型，body中选择raw，格式选择JSON，执行后，数据在[**数据库**](javascript:;)中可查

[![img](http://www.51testing.com/attachments/2017/08/15201284_2017080715025417no1.png)](http://www.51testing.com/batch.download.php?aid=72177)[![img](http://www.51testing.com/attachments/2017/08/15201284_201708071503001PMmT.png)](http://www.51testing.com/batch.download.php?aid=72178)[![img](http://www.51testing.com/attachments/2017/08/15201284_201708071503171pQIx.png)](http://www.51testing.com/batch.download.php?aid=72179)

　　上面的效果，通过python的requests和json模块，同样可以实现

　　json的dumps方法可以将json格式数据序列为python的相关数据类型

[![img](http://www.51testing.com/attachments/2017/08/15201284_201708071503311aQYY.png)](http://www.51testing.com/batch.download.php?aid=72180)