# 第16章 Postman常用测试结果验证及使用技巧

[TOC]

　　[**Postman**](javascript:;)的test本质上是JavaScript代码，通过我们编写[**测试**](javascript:;)代码，每一个tests返回True,或是False。

　　每一个tests实际上就是一个[**测试用例**](javascript:;)

　　官方文档给出了很多验证方式，我们通过实例来进行学习

　　接口返回结果为json

  [![img](http://www.51testing.com/attachments/2018/03/14982672_201803061358181mn7A.jpg)](http://www.51testing.com/batch.download.php?aid=83726)

## 1.检查response的body中是否包含字符串

　　tests["测试点"]=responseBody.has("需要查找的字符串");

　　例：

　　tests["statuscode"]=responseBody.has("301");

　　tests["status是否存在"]=responseBody.has("status");

　　tests["lists是否存在"]=responseBody.has("lists");

　　tests["lists值为11"]=responseBody.has("11");

　　注：当json中value为integer时，需要查找的值可以不带双引号，

　　tests["xxx"]xxx代表的是你测试点的名字，可以是中文

　　tests["xxx"]xxx在一个脚本中如果出现多次，那么只执行第一个，所以尽量不要重复

　　当value等于中文字符串时，这个方法貌似就不怎么好用了，但是我们有别的方法去验证，往下看，如果有读者知道怎么解决这个问题，也可以联系我，教教我

## 2.检查ResponseBody是否等于字符串

　　tests["测试点"]=responseBody==="ResponseBody返回的内容";

　　这个可以用在接口返回内容为纯字符串时，直接检查整个返回结果的正确性，

　　例子：

　　接口返回：哈哈

　　tests["返回为哈哈"]=responseBody==="哈哈";

　　tests["返回为哈哈"]=responseBody==="哈";

　　第二个会返回False，必须完全匹配

## 3.检查相应时间

　　tests["Responsetime小于200毫秒"]=responseTime>200;

　　tests["Responsetime大于200毫秒"]=responseTime<200;

## 4.检查状态码

　　这个也好理解，就是http请求状态码

　　tests["Statuscodeis200"]=responseCode.code===200;

　　注：

　　这里的状态码，跟上面我们用的json里边的"status"不是一回事

## 5.Codenamecontainsastring

　　tests["Statuscodenamehasstring"]=responseCode.name.has("Created");

　　tests["502"]=responseCode.name.has("Server");

　　tests["502"]=responseCode.name.has("UnreachableServer");

　　这个我的理解是，检查HTTPcode对应的string，如下面给出的list

　　如下对应表，如果使用fiddler模拟相应的返回，注意fiddler返回的大小写有问题，用下表的string

　　1)消息（1字头）

　　100Continue

　　2)成功（2字头）

　　200OK

　　3)重定向（3字头）

　　300MultipleChoices

　　301MovedPermanently

　　302Movetemporarily

　　。。。。。

　　500InternalServerError

　　501NotImplemented

　　502BadGateway

　　503ServiceUnavailable

　　600UnparseableResponseHeaders（省略了一些）

## 6.设置环境变量/全局变量

　　postman.setEnvironmentVariable("key","value");

　　postman.setGlobalVariable("key","value");

## 7.把XML的body转换成JSON对象：

　　varjsonObject=xml2Json(responseBody);

## 8.检查json的值

　　varjsonData=JSON.parse(responseBody);tests["Yourtestname"]=jsonData.value===100;

　　还拿上面的json数据做测试

　　tests["状态码为301"]=jsonData["status"]=="301";

　　tests["message"]=jsonData["message"]=="购买商品库存不足";

　　tests["list"]=jsonData["lists"][0]=="11";

## 9.检查有信息

　　tests["Content-Typeispresent"]=postman.getResponseHeader("content-Type");//不区分大小写

　　tests["Content-Typeispresent"]=responseHeaders.hasOwnProperty("Content-Type");//区分大小写

## 10.POSTrequest状态码

　　tests["SuccessfulPOSTrequest"]=responseCode.code===201||responseCode.code===202;

　　201-Created服务器已经创建了文档，Location头给出了它的URL。

　　202-Accepted已经接受请求，但处理尚未完成。

　　官方文档中还给出了对于json的验证例子

　　这种基于JSON格式定义JSON数据结构的规范，我们叫他JSONSchema

## 官方例子

　　varschema={"items":{"type":"boolean"}};vardata1=[true,false];vardata2=[true,123];console.log(tv4.error);tests["ValidData1"]=tv4.validate(data1,schema);tests["ValidData2"]=tv4.validate(data2,schema);

　　data1和data2是测试数据，schema相当于验证json的规范

　　示例中验证data1和data2中的value是否都是boolean类型

　　先了解下书写json规范文档常用的关键字

[![img](http://www.51testing.com/attachments/2018/03/14982672_201803061358182ekh4.jpg)](http://www.51testing.com/batch.download.php?aid=83727)

　　还拿第一个json做例子
```
{
"$schema":"http://json-schema.org/draft-04/schema#",
"id":"",
"properties":{
"lists":{
"id":"",
"items":{
"default":11,
"description":"检查list值",
"id":"",
"title":"",
"type":"integer"
},
"type":"array"
},
"message":{
"default":"购买商品库存不足",
"description":"message信息",
"id":"",
"title":"",
"type":"string"
},
"status":{
"default":301,
"description":"返回状态值",
"id":"",
"title":"",
"type":"integer"
}
},
"type":"object"
}
```
上文内容不用于商业目的，如涉及知识产权问题，请权利人联系博为峰小编(021-64471599-8017)，我们将立即处理。

　　一个完整的JSONSchema验证规范

　　可以根据实际情况删除一些key，但是红色标记的要保留

　　default默认值，根据实际情况书写，上面例子“商品库存不足时”的状态码为301，如果要对status和message的值进行验证，那么default就可以加上，如果只是验证返回的value是integer或是string类型，可以忽略

　　还可以加入最大值最小值等限制
　　下面是测试代码
```
varjsonData=JSON.parse(responseBody);
varschema={
"properties":{
"lists":{
"items":{
"default":11,
"description":"库存不足的商品id",
"type":"integer"
},
"type":"array"
},
"message":{
"default":"购买商品库存不足",
"description":"id为11的商品库存不足",
"type":"string"
},
"status":{
"description":"status",
"type":"integer"
}
},
"type":"object"
};
```
　　tests["json格式验证"]=tv4.validate(jsonData,schema);//验证json格式

　　tests["返回状态码是200"]=responseCode.code===200;

　　tests["状态码为301"]=jsonData["status"]=="301";

　　tests["message"]=jsonData["message"]=="购买商品库存不足";

　　tests["list"]=jsonData["lists"][0]=="11";

　　这样接口返回的json结构和数据我们就可以验证了。

　　tv4为Postman引入的外部库，想了解的可以去看官方文档

　　**另外Postman还提供了一些方法如：**

　　responseCookies

　　request.data["key"]=="value"

　　request.headers["key"]=="value"

　　request.method

　　request.url

　　request

　　responseHeaders

　　responseBody

　　responseTime

　　responseCode包含code，name，detail

　　iteration

　　这些方法可以帮助我们做更多的事情，比如通过一个接口拿到cookie值，然后把cookie设置成全局变量，提供给其他接口使用

　　当我们写测试脚本时，可能会遇到脚本书写错误或是需要一些log来辅助我们完善脚本，我们可以打开View->ShowPostmanConsole，打开后我们可以通过console.log(xxx)来输出日志和查看错误信息

　　通过上面这些知识，我们可以解决大多数的问题，如果想更进一步，需一定的js基础