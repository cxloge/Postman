# 第12章 你应该学会的接口调试神器—Postman高级用法

[TOC]

　[**postman**](javascript:;)这个神器相信大家都用过，程序员作为非专业的[**测试**](javascript:;)人员，非常需要这么一款简单轻量级的restful测试工具，但是不知道你是否知道，postman的强大之处不只是测试一下接口，还有其他非常赞的使用方式。

## 批量执行接口

　　入门级功能，但是被很多人忽略。postman左侧有个collections的tab,可以将接口进行分组，而且可以将分组以后的接口进行批量的执行，是一个非常赞的功能。当然，点击Runner也是可以的。

### 批量执行入口

　　[![img](http://www.51testing.com/attachments/2018/01/14982672_201801081344351OkWM.jpg)](http://www.51testing.com/batch.download.php?aid=80326)

### 批量执行界面

　　[![img](http://www.51testing.com/attachments/2018/01/14982672_201801081344352prHo.jpg)](http://www.51testing.com/batch.download.php?aid=80327)

　　可以设置环境、重复次数、每个接口延迟等，并且会显示批量执行的结果。

　　这个是非常基础的功能，有了这个基础以后，批量的测试以及自动化的测试都可以实现。

### 认证authorization

　　接口认证是所有接口必须做的事情，postman已经帮我们帮一些常用的接口认证机制可视化了，使用起来非常简单。

　　加入需要用的基础的auth认证，不管是auth1.0,还是auth2.0都能很好的支持。

[![img](http://www.51testing.com/attachments/2018/01/14982672_201801081344353Fryg.jpg)](http://www.51testing.com/batch.download.php?aid=80328)

[![img](http://www.51testing.com/attachments/2018/01/14982672_201801081344354Pnc8.jpg)](http://www.51testing.com/batch.download.php?aid=80329)

　　当然，有的时候认证方式完全是自定义的，在authorization功能找不到认证的方式,例如很多的身份认证是需要通过时间戳、密码或者其他参数根据一定的算法规则，算出一个结果，那么是不是我们就没有办法使用了？当然不是，那就需要重点介绍的功能——postman脚本，但这之前，我们先介绍一下还有一个非常重要的概念：环境变量

### 环境变量

　　对于一个程序员来说，环境变量这个概念还是很好理解，这里的环境变量就是大家理解的那样了，设置了环境变量以后，所有的接口都可以使用这个变量，而且这个变量是可以通过代码进行修改的。

　　设置环境变量：

　　postman.setEnvironmentVariable("sign", mdmauth.toString());

　　使用如上环境变量，只要在参数中用{{sign}}，如图：

　　[![img](http://www.51testing.com/attachments/2018/01/14982672_201801081344355WVE3.jpg)](http://www.51testing.com/batch.download.php?aid=80330)

### 执行前脚本

　　postman界面有个名叫pre-request script 的tab，从这里开始就介绍一下postman最重要的功能之一，脚本功能。pre-request script就是在请求之前执行的脚本。

　　[![img](http://www.51testing.com/attachments/2018/01/14982672_2018010813443568Hdy.jpg)](http://www.51testing.com/batch.download.php?aid=80331)

　　执行前脚本我一般的用法就是用来修改环境变量，因为执行前做的事情，主要就是对请求的参数做一些处理。这里举个简单的例子：

　　某接口的接口认证规则，主要是通过header中的authentication来进行身份的认证，authentication的值是根据秘钥（key）,时间戳（timeStamp），传入的参数（param），以及key、timeStamp和param组成生成字符串md5以后生成的sign，最终的结果类似于：

　　{"timeStamp": "2017-11-13 10:06:08",sign": "99f8d869d6a105afddd9d152c5894418"}

　　其实这是一个很常用场景，很多接口都是当前的参数和时间戳联合进行处理，来确保接口参数时效性，这样的场景直接通过参数或者环境变量肯定是有问题的，因为时间是动态的，只能动过程序来处理。我来处理方式大概就是：

　　· 脚本计算出需要的值，将值设为环境变量

　　· 参数设置的value为当前的环境变量

　　· 执行测试

　　脚本如下：
```
var date=new Date();
var y = date.getFullYear();
var m = date.getMonth() + 1;
m = m < 10 ? ('0' + m) : m;
var d = date.getDate();
d = d < 10 ? ('0' + d) : d;
var h = date.getHours();
h=h < 10 ? ('0' + h) : h;
var minute = date.getMinutes();
minute = minute < 10 ? ('0' + minute) : minute;
var second=date.getSeconds();
second=second < 10 ? ('0' + second) : second;
//获取时间，格式为yyyy-mm-dd HH:mm:ss
var timespan=y + '-' + m + '-' + d+' '+h+':'+minute+':'+second;
var key='dfc96ds8-e5a0-45aa-a2ec-2611cds71d4e';
//通过request.data获取body的内容，这个是postman内置变量
var param=request.data;
console.log(key);
console.log(timespan);
console.log(param);
//CryptoJS,postman的内置js库
var sign=CryptoJS.MD5(key+timespan+param).toString();
console.log(sign);
var mdmauth="{\"timeStamp\": \""+timespan+"\",\"sysCode\": \"EUH\",\"sign\": \""+sign+"\"}";
console.log(mdmauth);
//设置环境变量
postman.setEnvironmentVariable("mdmauth", mdmauth.toString());
```
　　postman的脚本是大家非常熟悉的javascript脚本，而且postman还内置了一些重用的js库，基本能满足所有的使用场景，我们常用内置的函数包括：

　　· Lodash，一个基础的函数库，大家应该都用过

　　· cheerio，可以理解为另一个jquery

　　· BackboneJS,js的mvc框架

　　· CryptoJS，js加密库，支持几乎所有的常用加密方式

　　使用过程中我们也需要获取请求的值，或者请求的结果，post有几个内置的变量可以直接获取：

　　· request 获取请求的参数，包括头和请求体

　　· responseHeaders 返回值的header

　　· responseBody 返回值的body

　　· responseCode 返回值的http code

　　除此之外，还有几个内置的全局动态环境变量：

　　· {{$guid}}: 生成一个guid

　　· {{$timestamp}}: 获取当前时间戳

　　· {{$randomInt}}: 获取一个动态整数

　　说真的，postman考虑的是在是太周到了，有了以上的神器，不只是可以自动化的编写脚本，而且还能非常方便的编写脚本，测试任何类型的接口。

　　具体内容，建议详细阅读：https://www.getpostman.com/docs/postman/scripts/postman_sandbox ，这个页面的内容非常重要。

### 测试脚本

　　前文介绍了批量执行接口，执行前脚本能相关内容，只要能支持编程，接口的测试就变得很灵活，容易定制。其实，正常的测试还有一个场景，接口的测试都是有依赖的，如接口的测试都依赖于token接口来获取脚本，或者批量测试的时候，后面的接口需要前面接口的返回值等，postman肯定也是支持的，批量执行接口结合测试脚本，使用就非常简单了。

　　测试的代码在Test这个tab中，这里的结果是测试完成后执行的内容。pre-request script是执行前，test是执行后，这样就能构成一个闭环了。（完美！！！）

　　[![img](http://www.51testing.com/attachments/2018/01/14982672_201801081344357c3cR.jpg)](http://www.51testing.com/batch.download.php?aid=80332)

　　示例代码：
```
var jsonData = JSON.parse(responseBody);
//tests的内容会在测试的时候展示
tests["http code"] = responseCode.code === 200;
tests["返回值正常"] = jsonData.Result===true;
postman.setEnvironmentVariable("authtoken",CryptoJS.MD5(request.headers["UserName"]+jsonData.Data.FranchiseeCode));
//执行成功后调用下一个接口
postman.setNextRequest("获取待处理");
```
　　其中，有个函数postman.setNextRequest 会调用下一个接口，这两就可以让接口执行的有顺序，这就是我们需要的流程测试。

### 调试

　　既然涉及到编程，那么肯定也会涉及到调试，postman对调试的支持也是非常好的，只需要简单的设置，结合chrome就能进行调试。

　　首先，开启下chrome的调试。在chrome地址栏中输入：chrome://flags/#debug-packed-apps ，开启Debugging for packed app。（设置栏目较多，建议搜索找到）

　　[![img](http://www.51testing.com/attachments/2018/01/14982672_201801081344358NHRx.jpg)](http://www.51testing.com/batch.download.php?aid=80333)

　　接着，输入chrome://inspect/#apps，选择postman的inspect，就弹出我们熟悉的postman的调试框

[![img](http://www.51testing.com/attachments/2018/01/14982672_201801081344359bNjS.jpg)](http://www.51testing.com/batch.download.php?aid=80334)

　　我们在postman中的console.log或者断点都是可以进行调试的，和chrome调试[**web**](javascript:;)一样的。

## 总结

　　以上只是介绍了部分关于postman使用中，稍微高级一点的功能，其实postman还有很多好的功能，如文档导出、纯脚本测试，这些功能如果大家有用到，建议仔细阅读官网的doc，postman绝对不是简单的一个测试接口的工具，是一个完全覆盖开发人员测试场景的接口调试工具。