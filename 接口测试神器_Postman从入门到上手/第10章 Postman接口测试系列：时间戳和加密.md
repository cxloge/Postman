# 第10章 Postman接口测试系列：时间戳和加密

　　在使用[**postman**](javascript:;)进行[**接口测试**](javascript:;)的时候，对于有些接口字段需要时间戳加密，这个时候我们就遇到2个问题，其一是接口中的时间戳如何得到？其二就是对于现在常用的md5加密操作如何在postman中使用代码实现呢？

　　**下面我们以一个具体的接口例子来进行说明。**

　　首先来看看我们的接口文档信息，如图所示

[![img](http://www.51testing.com/attachments/2017/12/14982672_201712011145111Fv6K.png)](http://www.51testing.com/batch.download.php?aid=78417)

　　此接口文档中，需要三个参数customercode、timestamp和itoken（是customerCode+timestamp+ytoken加密后的结果）。

　　第一次操作的时候，我们使用postman会这样操作，如图

　[![img](http://www.51testing.com/attachments/2017/12/14982672_201712011145112oRRr.png)](http://www.51testing.com/batch.download.php?aid=78418)

　　这样操作流程是：

　　1、选择提交方式是post，输入接口的url地址

　　2、选择接口情况的方式是x-www-form-urlencoded

　　3、设置接口的参数customerCode、timestamp和itoken和值

　　4、设置完成之后点击send发送，查看接口响应结果

　　**说明**

　　x-www-form-urlencoded即是application/x-www-from-urlencoded，将表单内的数字转换为键对值

　　postman中 form-data、x-www-form-urlencoded、raw、binary的区别：

　　http://blog.csdn.net/ye1992/article/details/49998511

　　时间戳转换工具：

　　http://tool.chinaz.com/Tools/unixtime.aspx

　　md5加密工具：

　　https://md5jiami.51240.com/

　　这样创建会话的接口我们就完成了！但是为了系统的安全性，这里的timestamp是每30分钟就会过期的，下次我们又需要重新设置timestamp，就是md5加密的结果......这样操作岂不是太麻烦?

　　还好postman中Pre-Request Script可以在 Request 之前自定义请求数据，这样做的好处就是可以以嵌入脚本的方式动态准备测试数据，并根据业务需求设计[**测试用例**](javascript:;)。

　　这里我们仍继续以上面的用例为例：

　　在postman中，如何才能获取当前机器上的timestamp呢？

　　Math.round(new Date().getTime())

　　可以满足我们的要求!!!

　　那代码如何实现呢？

　　//设置当前时间戳毫秒

　　postman.setGlobalVariable("timestamp",Math.round(new Date().getTime()));

　　这样就将获取的时间戳设置为全局变量timestamp

　　我们知道itoken的值是md5(customerCode+timestamp+ytoken')

　　那么接下来就可以动态的获取md5的信息了，代码如下:
```
//发起请求之前获取当前的时间戳放在参数里
//postman.setGlobalVariable("customerCode","***2345677***");
//1.设置环境变量 postman.setEnvironmentVariable("key", "value");
//2.设置全局变量 postman.setGlobalVariable("key", "value");
//environment.customerCode = "***2345677***";
customerCode = postman.getGlobalVariable("customerCode");
//设置当前时间戳毫秒
postman.setGlobalVariable("timestamp",Math.round(new Date().getTime()));
//environment.timestamp = Math.round(new Date().getTime());
//postman.setEnvironmentVariable("unixtime_now","timecode");
//var jsonData = JSON.parse(request.data.applyJsonStr);
//postman.setGlobalVariable("ytoken","*********b176a4739bfccb*********");
//获取全局变量
//如postman.getGlobalVariable("key");
customerCode = postman.getGlobalVariable("customerCode");
timestamp = postman.getGlobalVariable('timestamp');
ytoken = postman.getGlobalVariable("ytoken");
var str = customerCode+timestamp+ytoken;
//postman.setEnvironmentVariable("str",str);
//environment.str = str;
postman.setGlobalVariable("str",str);
//var md5 = CryptoJS.MD5(str).toString().toLowerCase();
//使用md5加密
//var strmd5 = CryptoJS.MD5(str).toString();
var strmd5 = CryptoJS.MD5(str);
//environment.strmd5 = strmd5;
postman.setGlobalVariable('md5',strmd5);
//environment.md5 = md5;
//timecode=System.currentTimeMillis();
console.log(str);
```
　　而在接口请求中，就可以使用已经定义好的变量来进行接口操作，代码如下
```
customerCode:{{customerCode}}
timestamp:{{timestamp}}
ltoken:{{md5}}
```
　　如图所示

[![img](http://www.51testing.com/attachments/2017/12/14982672_201712011145113O5dl.png)](http://www.51testing.com/batch.download.php?aid=78419)

　　这样下次创建接口的时候，直接运行该用例即可，不用再次修改参数值~(≧▽≦)/~

　　那么我们如何才能知道该接口用例是成功的呢，该怎么断言呢？

　　这里列出我该接口断言的一个示例，代码如下
```
/*
// 推荐用全等 ===，确保类型和值都一致
tests['Status code is 200'] = responseCode.code === 200;
// 判断是否存在 'success' 值
tests["Body matches code"] = responseBody.has("0");
var jsonData = JSON.parse(responseBody);
postman.setEnvironmentVariable("sessionId",jsonData.result);
tests[`[INFO] Request params: ${JSON.stringify(request.data)}`] = true;
tests["have result "]=jsonData.hasOwnProperty("error")!==true;
tests[`[INFO] Response timeout: ${responseTime}`] = responseTime < 6000;
**/
//状态代码是200
if(responseCode.code === 200){
// 判断是否存在 'success' 值，检查响应体包含一个字符串
tests["Body matches code"] = responseBody.has("0");
//响应结果中result保存为全局变量sessonId
var jsonData = JSON.parse(responseBody);
postman.setGlobalVariable("sessionId",jsonData.result);
//输入接口参数信息
tests[`[INFO] Request params: ${JSON.stringify(request.data)}`] = true;
// tests["have result "]=jsonData.hasOwnProperty("error")!==true;
//判断接口响应结果有result
tests["have result "]=jsonData.hasOwnProperty("result")===true;
//判断接口响应时间小于N秒
tests[`[INFO] Response timeout: ${responseTime}`] = responseTime < 6000;
}else{
//接口请求失败
tests["Waring：Request Failed. Please Fix!"] = false;
}
```
　　这样创建会话的接口就完成了！