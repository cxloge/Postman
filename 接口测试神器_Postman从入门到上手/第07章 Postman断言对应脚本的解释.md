# 第07章 Postman断言对应脚本的解释

[TOC]

## 内置脚本说明

[![img](http://www.51testing.com/attachments/2018/03/14982672_201803051024531W0Yy.png)](http://www.51testing.com/batch.download.php?aid=83656)

### 1.清除一个全局变量

　　Clear a global variable

　　对应脚本：

　　[**postman**](javascript:;).clearGlobalVariable("variable_key");

　　参数：需要清除的变量的key

### 2.清除一个环境变量

　　Clear an environment variable

　　对应脚本：

　　postman.clearEnvironmentVariable("variable_key");

　　参数：需要清除的环境变量的key

### 3.response包含内容

　　Response body:Contains string

　　对应脚本：

　　tests["Body matches string"] =responseBody.has("string_you_want_to_search");

　　参数：预期内容

### 4.将xml格式的response转换成son格式

　　Response body:Convert XML body to a JSON Object

　　对应脚本：

　　var jsonObject = xml2Json(responseBody);

　　参数：（默认不需要设置参数,为接口的response）需要转换的xml

### 5.response等于预期内容

　　Response body:Is equal to a string

　　对应脚本：

　　tests["Body is correct"] = responseBody === "response_body_string";

　　参数：预期response

### 6.json解析key的值进行校验

　　Response body:JSON value check

　　对应脚本：

　　tests["Args key contains argument passed as url parameter"] = 'test' in responseJSON.args

　　参数：test替换被测的值，args替换被测的key

### 7.检查response的header信息是否有被测字段

　　Response headers:Content-Type header check

　　对应脚本：

　　tests["Content-Type is present"] = postman.getResponseHeader("Content-Type");

　　参数：预期header

### 8.响应时间判断

　　Response time is less than 200ms

　　对应脚本：

　　tests["Response time is less than 200ms"] = responseTime < 200;

　　参数：响应时间

### 9.设置全局变量

　　Set an global variable

　　对应脚本：

　　postman.setGlobalVariable("variable_key", "variable_value");

　　参数：全局变量的键值

### 10.设置环境变量

　　Set an environment variable

　　对应脚本：

　　postman.setEnvironmentVariable("variable_key", "variable_value");

　　参数：环境变量的键值

### 11.判断状态码

　　Status code:Code is 200

　　对应脚本：

　　tests["Status code is 200"] = responseCode.code != 400;

　　参数：状态码

### 12.检查code name 是否包含内容

　　Status code:Code name has string

　　对应脚本：

　　tests["Status code name has string"] = responseCode.name.has("Created");

　　参数：预期code name包含字符串

### 13.成功的post请求

　　Status code:Successful POST request

　　对应脚本：

　　tests["Successful POST request"] = responseCode.code === 201 || responseCode.code === 202;

### 14.微小验证器

　　Use Tiny Validator for JSON data

　　对应脚本：

　　参数：可以修改items里面的键值对来对应验证json的参数

## 举例说明

### 发送一个get请求

　　Postman安装完成后，我们来用它向[**百度**](javascript:;)发送一个搜索请求。比如搜“Postman”吧。

　　我们先在百度搜索框输入“Postman”，点击“百度一下”，然后将[**浏览器**](javascript:;)地址栏的内容复制到Postman的请求地址栏，点击Send。这样，我们就向百度首页发送了一个搜索请求，这个请求是GET请求，如下图所示。从图中，我们可以看到本次请求的状态码Status是200，表示此次请求发送成功。本次的请求响应时间是321ms，另外还可以响应的HTML文档。

[![img](http://www.51testing.com/attachments/2018/03/14982672_201803051024532nPiD.png)](http://www.51testing.com/batch.download.php?aid=83657)

### 修改请求的参数

　　在上图中点击Params，Postman将会把url中的所有参数解析成一个一个的key-vaule对，如下图所示。其中wd这个key对应的value是postman。我们将其改成“Chrome”，再次点击Send。请求的结果将变成搜索“Chrome”的页面HTML。

[![img](http://www.51testing.com/attachments/2018/03/14982672_201803051024533tqKP.png)](http://www.51testing.com/batch.download.php?aid=83658)

### 验证请求结果

　　验证返回的页面中包括指定的字符串：页面中包括“Chrome”。

　　点击地址栏下面的Tests选项卡，进入Tests脚本编写页面。点击“Response body: Contains string”，将“string_you_want_to_search”替换成“Chrome”。点击Send发送请求，执行[**测试**](javascript:;)。在下方Response区域的Test选项卡里，可以看到Pass “Body matches string”，表示该请求的响应体重包含“Chrome”字符串，测试通过。

[![img](http://www.51testing.com/attachments/2018/03/14982672_201803051024534SG8c.png)](http://www.51testing.com/batch.download.php?aid=83659)

　　不通过测试显示如下

[![img](http://www.51testing.com/attachments/2018/03/14982672_2018030510245357NHR.png)](http://www.51testing.com/batch.download.php?aid=83660)