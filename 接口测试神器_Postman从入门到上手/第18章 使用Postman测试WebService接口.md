# 第18章 使用Postman测试WebService接口

[TOC]

## 我们拿SOAP 1.1的方法来举例（简体字转换为繁体字）

　[![img](http://www.51testing.com/attachments/2018/02/14982672_201802080951551g4FH.jpg)](http://www.51testing.com/batch.download.php?aid=82551)　

WebService

## **关于SOAP**

　　它是基于XML的的简易协议，在HTTP的基础上进行信息交换（一般是使用POST请求）

## 使用Postman测试WebService？

### 1.输入WebService地址，请求方式为POST

　　[![img](http://www.51testing.com/attachments/2018/02/14982672_2018020809515525A89.jpg)](http://www.51testing.com/batch.download.php?aid=82552)

WebService地址

### 2.添加请求头

　　上面我们提到过SOAP是基于XML的格式来进行传输的，这边需要指定传输数据的类型；并且指定了数据编码格式为UTF-8（中文乱码）

　[![img](http://www.51testing.com/attachments/2018/02/14982672_201802080951553tZW0.jpg)](http://www.51testing.com/batch.download.php?aid=82553)　

添加请求头

### 3.上传数据并发送请求

　　这边把接口定义的请求格式复制进去，填上必要的参数就可以了；注意的是这边要选择raw得方式进行请求，关于它们的区别我在后面会写到。

　　[![img](http://www.51testing.com/attachments/2018/02/14982672_201802080951554sqs7.jpg)](http://www.51testing.com/batch.download.php?aid=82554)

上传数据并发送请求

## 关于上面这四种请求方式

### · form-data

　　相当于Content-Type:multipart/form-data;

　　它会将表单的数据处理为一条消息，以标签为单元，用分隔符分开。既可以上传键值对，也可以上传文件。

　　[![img](http://www.51testing.com/attachments/2018/02/14982672_201802080951555ee86.jpg)](http://www.51testing.com/batch.download.php?aid=82555)

### · x-www-form-urlencoded

　　相当于application/x-www-from-urlencoded，会将表单中的数据以键值对的形式拼接起来；如：name=许渺&gender=0

　　[![img](http://www.51testing.com/attachments/2018/02/14982672_201802080951556y0f3.jpg)](http://www.51testing.com/batch.download.php?aid=82556)

### · raw

　　上传任意格式的文本，比如JSON、XML等

　　[![img](http://www.51testing.com/attachments/2018/02/14982672_201802080951557rWno.jpg)](http://www.51testing.com/batch.download.php?aid=82557)

### · binary

　　相当于Content-Type:application/octet-stream；用来上传二进制数据，一般是用来上传文件；因为没有键值对所以每次只能上传一个文件。

[![img](http://www.51testing.com/attachments/2018/02/14982672_201802080951558GTk6.jpg)](http://www.51testing.com/batch.download.php?aid=82558)