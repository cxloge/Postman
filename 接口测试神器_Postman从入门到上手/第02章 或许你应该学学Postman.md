# 第02章 或许你应该学学Postman

[TOC]

## 简单模拟请求的工具

[![img](http://www.51testing.com/attachments/2018/03/14982672_201803021354021jo34.png)](http://www.51testing.com/batch.download.php?aid=83632)

## 使用

　　最简单的方法就是直接在[**浏览器**](javascript:;)中复制 Copy as cURL ，然后把数据导入 [**postman**](javascript:;)，然后 send ，收工。

### 我们这里拿 知乎首页 举例

![img](http://www.51testing.com/attachments/2018/03/14982672_2018030213550513u3B.png)](http://www.51testing.com/batch.download.php?aid=83633)

### 在对应的请求下复制 cURL

　　打开 postman ， 点击左上角的 Import ， 选择Paste Raw Text ，最后 Import，点击 send发送请求

[![img](http://www.51testing.com/attachments/2018/03/14982672_201803021355052pe0k.png)](http://www.51testing.com/batch.download.php?aid=83634)

　　发送请求之后就可以查看了，如下图，标箭头的地方可以打开看更多。比如可以预览[**web**](javascript:;)界面，查看 Headers 信息，查看状态，复制代码。

[![img](http://www.51testing.com/attachments/2018/03/14982672_201803021355053jnI6.png)](http://www.51testing.com/batch.download.php?aid=83635)

　　同时可以打开 Headers ，用来调试，哪些是需要的，哪些不需要

[![img](http://www.51testing.com/attachments/2018/03/14982672_201803021355054hHbw.png)](http://www.51testing.com/batch.download.php?aid=83636)

　　最方便的一点是，可以直接生成对应的编程语言，并复制，例如[**Python**](javascript:;)的requests方法：

　　好了，到这里 postman 的简单功能就说完了，他的全部功能当然不止这一点，更多的就去看 文档啦

### 问题

　　在我的使用过程中，发现了 postman 的一些问题，如：导入错误，参数错误，请求失误。

### 导入错误

　　例如知乎这个例子，如果我们复制的是 Copy as cURL (cmd) ，可能你会遇到下面的错误

[![img](http://www.51testing.com/attachments/2018/03/14982672_201803021355055Kawn.png)](http://www.51testing.com/batch.download.php?aid=83637)

　　这个时候选用 Copy as cURL (bush) 就好了，具体原因是啥，我也不清楚。我在这里找到了别人的描述

　　There is no difference between the two cURL command because there is a difference between ” and ‘.

　　Refer : Use cURL to get the same results as a web browser

　　参数错误

　　举个例子，今天在帮朋友查看 这个网站 的翻页，复制用postman打开， copy cURL 内容是

```
curl "https://www.crunchbase.com/v4/data/entities/organizations/56e40f50-97c7-2a77-255d-1d97d5f30646/overrides?field_ids=^%^5B^%^22identifier^%^22,^%^22layout_id^%^22,^%^22facet_ids^%^22,^%^22title^%^22,^%^22short_description^%^22,^%^22is_locked^%^22^%^5D^&card_ids=^%^5B^%^22investments_list^%^22^%^5D" -H "cookie: _ga=GA1.2.35962729.1517412509; _gid=GA1.2.2072770006.1517412509; _vdl=1; _hp2_ses_props.973801186=^%^7B^%^22ts^%^22^%^3A1517412512548^%^2C^%^22d^%^22^%^3A^%^22www.crunchbase.com^%^22^%^2C^%^22h^%^22^%^3A^%^22^%^2Fsearch^%^2Fprincipal.investors^%^22^%^7D; __qca=P0-1969245879-1517412512628; D_IID=1B7344D2-1C8F-3327-8607-D786306444AE; D_UID=208F925B-3D1C-3491-A532-C82375EE187D; D_ZID=497DB63C-5101-3F49-BE35-1752A80F8DDA; D_ZUID=D89FCBAA-BF79-340C-BF55-B860768D0993; D_HID=57B19D5F-5069-3A82-94CB-D42821D1CD10; D_SID=123.120.141.63:bXaeU41PWi5vyYIflFmiShQiK1qwq/nC4G9IljWo+6A; AMCVS_6B25357E519160E40A490D44^%^40AdobeOrg=1; wcsid=KZbgLoopx4WnyMOW3F6pZ0H92JEzMrBd; hblid=cfw6lOKzm4FpCUou3F6pZ0H92JE6rBWB; s_cc=true; AMCV_6B25357E519160E40A490D44^%^40AdobeOrg=1099438348^%^7CMCMID^%^7C05859477990281579603868663655860142263^%^7CMCAAMLH-1518017313^%^7C11^%^7CMCAAMB-1518017313^%^7CRKhpRz8krg2tLO6pguXWp5olkAcUniQYPHaMWWgdJ3xzPWQmdj0y^%^7CMCOPTOUT-1517419713s^%^7CNONE^%^7CMCAID^%^7CNONE^%^7CMCSYNCSOP^%^7C411-17570^%^7CvVersion^%^7C2.1.0; _okdetect=^%^7B^%^22token^%^22^%^3A^%^2215174125149410^%^22^%^2C^%^22proto^%^22^%^3A^%^22https^%^3A^%^22^%^2C^%^22host^%^22^%^3A^%^22www.crunchbase.com^%^22^%^7D; olfsk=olfsk8562990481377502; _okbk=cd4^%^3Dtrue^%^2Cvi5^%^3D0^%^2Cvi4^%^3D1517412515909^%^2Cvi3^%^3Dactive^%^2Cvi2^%^3Dfalse^%^2Cvi1^%^3Dfalse^%^2Ccd8^%^3Dchat^%^2Ccd6^%^3D0^%^2Ccd5^%^3Daway^%^2Ccd3^%^3Dfalse^%^2Ccd2^%^3D0^%^2Ccd1^%^3D0^%^2C; _ok=1554-355-10-6773; _hp2_props.973801186=^%^7B^%^22Logged^%^20In^%^22^%^3Afalse^%^2C^%^22Pro^%^22^%^3Afalse^%^7D; _hp2_id.973801186=^%^7B^%^22userId^%^22^%^3A^%^228805156096536097^%^22^%^2C^%^22pageviewId^%^22^%^3A^%^221700148784936413^%^22^%^2C^%^22sessionId^%^22^%^3A^%^225929107734453151^%^22^%^2C^%^22identity^%^22^%^3Anull^%^2C^%^22trackerVersion^%^22^%^3A^%^223.0^%^22^%^7D; _oklv=1517412548852^%^2CKZbgLoopx4WnyMOW3F6pZ0H92JEzMrBd; s_pers=^%^20s_nrgvo^%^3DNew^%^7C1580484574965^%^3B" -H "origin: https://www.crunchbase.com" -H "accept-encoding: gzip, deflate, br" -H "x-distil-ajax: dfdvfavtsysazfberrtudvwabwe" -H "user-agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/63.0.3239.84 Safari/537.36" -H "content-type: application/json" -H "accept-language: zh-CN,zh;q=0.9,en;q=0.8" -H "accept: application/json, text/plain, */*" -H "referer: https://www.crunchbase.com/organization/500-startups/investments/investments_list" -H "authority: www.crunchbase.com" -H "x-requested-with: XMLHttpRequest" --data-binary ^"^{^
^\^"card_lookups^\^": ^[^
^{^
^\^"card_id^\^": ^\^"investments_list^\^",^
^\^"limit^\^": 100,^
^\^"after_id^\^": ^\^"07a9c686-4590-fa0f-3ac4-fc7b898c0b7a^\^"^
^}^
^]^
^}^" --compressed
```

​	导入之后，send，返回 400 错误。

　　postman 转义的code是：

```
import requests
url = "https://www.crunchbase.com/v4/data/entities/organizations/56e40f50-97c7-2a77-255d-1d97d5f30646/overrides"
querystring = {"field_ids":"^%^5B^%^22identifier^%^22,^%^22layout_id^%^22,^%^22facet_ids^%^22,^%^22title^%^22,^%^22short_description^%^22,^%^22is_locked^%^22^%^5D^","card_ids":"^%^5B^%^22investments_list^%^22^%^5D"}
payload = "^^{^\n\n  ^\\^card_lookups^^: ^[^\n\n    ^{^\n\n      ^\\^card_id^^: ^\\^investments_list^^,^\n\n      ^\\^limit^^: 100,^\n\n      ^\\^after_id^^: ^\\^07a9c686-4590-fa0f-3ac4-fc7b898c0b7a^^^\n\n    ^}^\n\n  ^]^\n\n^}^"
headers = {
'cookie': "_ga=GA1.2.35962729.1517412509; _gid=GA1.2.2072770006.1517412509; _vdl=1; _hp2_ses_props.973801186=^%^7B^%^22ts^%^22^%^3A1517412512548^%^2C^%^22d^%^22^%^3A^%^22www.crunchbase.com^%^22^%^2C^%^22h^%^22^%^3A^%^22^%^2Fsearch^%^2Fprincipal.investors^%^22^%^7D; __qca=P0-1969245879-1517412512628; D_IID=1B7344D2-1C8F-3327-8607-D786306444AE; D_UID=208F925B-3D1C-3491-A532-C82375EE187D; D_ZID=497DB63C-5101-3F49-BE35-1752A80F8DDA; D_ZUID=D89FCBAA-BF79-340C-BF55-B860768D0993; D_HID=57B19D5F-5069-3A82-94CB-D42821D1CD10; D_SID=123.120.141.63:bXaeU41PWi5vyYIflFmiShQiK1qwq/nC4G9IljWo+6A; AMCVS_6B25357E519160E40A490D44^%^40AdobeOrg=1; wcsid=KZbgLoopx4WnyMOW3F6pZ0H92JEzMrBd; hblid=cfw6lOKzm4FpCUou3F6pZ0H92JE6rBWB; s_cc=true; AMCV_6B25357E519160E40A490D44^%^40AdobeOrg=1099438348^%^7CMCMID^%^7C05859477990281579603868663655860142263^%^7CMCAAMLH-1518017313^%^7C11^%^7CMCAAMB-1518017313^%^7CRKhpRz8krg2tLO6pguXWp5olkAcUniQYPHaMWWgdJ3xzPWQmdj0y^%^7CMCOPTOUT-1517419713s^%^7CNONE^%^7CMCAID^%^7CNONE^%^7CMCSYNCSOP^%^7C411-17570^%^7CvVersion^%^7C2.1.0; _okdetect=^%^7B^%^22token^%^22^%^3A^%^2215174125149410^%^22^%^2C^%^22proto^%^22^%^3A^%^22https^%^3A^%^22^%^2C^%^22host^%^22^%^3A^%^22www.crunchbase.com^%^22^%^7D; olfsk=olfsk8562990481377502; _okbk=cd4^%^3Dtrue^%^2Cvi5^%^3D0^%^2Cvi4^%^3D1517412515909^%^2Cvi3^%^3Dactive^%^2Cvi2^%^3Dfalse^%^2Cvi1^%^3Dfalse^%^2Ccd8^%^3Dchat^%^2Ccd6^%^3D0^%^2Ccd5^%^3Daway^%^2Ccd3^%^3Dfalse^%^2Ccd2^%^3D0^%^2Ccd1^%^3D0^%^2C; _ok=1554-355-10-6773; _hp2_props.973801186=^%^7B^%^22Logged^%^20In^%^22^%^3Afalse^%^2C^%^22Pro^%^22^%^3Afalse^%^7D; _hp2_id.973801186=^%^7B^%^22userId^%^22^%^3A^%^228805156096536097^%^22^%^2C^%^22pageviewId^%^22^%^3A^%^221700148784936413^%^22^%^2C^%^22sessionId^%^22^%^3A^%^225929107734453151^%^22^%^2C^%^22identity^%^22^%^3Anull^%^2C^%^22trackerVersion^%^22^%^3A^%^223.0^%^22^%^7D; _oklv=1517412548852^%^2CKZbgLoopx4WnyMOW3F6pZ0H92JEzMrBd; s_pers=^%^20s_nrgvo^%^3DNew^%^7C1580484574965^%^3B",
'origin': "https://www.crunchbase.com",
'accept-encoding': "gzip, deflate, br",
'x-distil-ajax': "dfdvfavtsysazfberrtudvwabwe",
'user-agent': "Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/63.0.3239.84 Safari/537.36",
'content-type': "application/json",
'accept-language': "zh-CN,zh;q=0.9,en;q=0.8",
'accept': "application/json, text/plain, */*",
'referer': "https://www.crunchbase.com/organization/500-startups/investments/investments_list",
'authority': "www.crunchbase.com",
'x-requested-with': "XMLHttpRequest",
'cache-control': "no-cache",
'postman-token': "1df3b2b6-b682-edf7-4804-572ac5a03420"
}
response = requests.request("POST", url, data=payload, headers=headers, params=querystring)
print(response.text)
```

　　可以看到 加入了大量的 ^ 符号，这个在Python中是运算符

```
^按位异或运算符：当两对应的二进位相异时，结果为1(a ^ b) 输出结果 49 ，二进制解释： 0011 0001
```

　　这也是 postman 的一个问题

### 请求失误

　　这个问题，我也不是很懂，有的请求 postman 返回错误，但是复制代码到 Python 环境中运行是可以获得数据的，所以最好是多次验证。