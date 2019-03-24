# 第20章 Postman解决Token传参问题

[TOC]

## 问题描述：

　　有一个登陆接口获取token，其他接口再次访问都要带上token

## 解决方案：

　　1、在登陆接口访问后设置Postman的环境变量（Environment），例如设置环境变量名：token，值为登陆接口访问成功后，在responseBody中的token值，如何设置请看下面具体描述。

　　2、访问其他接口时token值直接读取变量即可。Postman里面获取变量的语法为：{{变量名}}

## 具体步骤：

### 1、登陆接口介绍

[![img](http://www.51testing.com/attachments/2018/03/14982672_201803061412031IuUF.png)](http://www.51testing.com/batch.download.php?aid=83728)

　　如图所示，login接口返回值JSON格式大体为：
```
{
"status": 0,
"message": "成功",
"data": {
"username": "cams_admin_dev",
"token": "eyJhbGciOiJIUzUxMiJ9.eyJleHAiOjE1MTYzNDIxMjAsInN1YiI6ImNhbXNfYWRtaW5fZGV2IiwiY3JlYXRlZCI6MTUxNjI1NTcyMDU0NywiZnVsbCI6ImNhbXNfYWRtaW5fZGV2IiwidWF1dGgiOiIvKio7QUxMIiwiYXV0aCI6InNldHRpbmdzLGNhbXNfYWRtaW4saW5kdXN0cnksYm9uZCxjYW1zSG9tZSxjb21wYW55LGFyZWEsZGV0YWlscyxjYW1zT3BlcmF0aW9uIn0.pI09X8KNoIK0fb6xC1xbrSZyg-EnUnlZ_9shmOQCRDtdIIEA5iyq3HmzgSx0ReaChEAZxkrrSRTtSXE8ZlbCTw"
}
}
```
　　返回值中有token值， 这个值怎么在访问login接口后自动设置为Postman环境变量呢？

### 2、在访问login接口后自动设置为Postman环境变量

　　在Postman软件的Tests中写以下代码，设置环境变量
```
pm.test("Status code is 200", function () {
pm.response.to.have.status(200);
});
// 把responseBody转为json字符串
var data = JSON.parse(responseBody);
// 设置环境变量token，供后面的接口引用
pm.environment.set("token", data.data.token);
```
　　如下图所示：

[![img](http://www.51testing.com/attachments/2018/03/14982672_201803061412032JJrJ.png)](http://www.51testing.com/batch.download.php?aid=83729)

　　点击Send按钮发送请求后，就可以动态设置环境变量名为token，值为token值的变量。

　　设置成功后，点击那个眼睛图标，查看变量如图所示：

[![img](http://www.51testing.com/attachments/2018/03/14982672_201803061412033cRFp.png)](http://www.51testing.com/batch.download.php?aid=83730)

### 3、访问其他接口，环境变量token

[![img](http://www.51testing.com/attachments/2018/03/14982672_2018030614120342BI5.png)](http://www.51testing.com/batch.download.php?aid=83731)

　　如图红色标注的所示

　　1) 另一个接口

　　2) TYPE中选择token的类型，我这里用到的是 Bearer Token

　　3) 右边红色标注的部分设置token值，格式为：{{token}}，获取前面login接口访问时动态设置的token，

　　那么这个接口就可以用了

　　点击Send会访问成功。