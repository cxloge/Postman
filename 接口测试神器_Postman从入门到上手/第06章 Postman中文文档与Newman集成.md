# 第06章 Postman中文文档与Newman集成

[TOC]

## 与Newman的命令行集成

​	Newman是[**Postman**](javascript:;)的命令行集合运行器。它允许您直接从命令行运行和测试Postman集合。它以可扩展性为基础构建，以便您可以轻松地将其与您的持续集成服务器集成并构建系统。

　　纽曼主要特性与Postman的功能类似，并允许您运行集合，只需在Postman应用程序的集合运行中执行集合。

　　Newman发布在 NPM registry 和 GitHub中。

　　[![img](http://www.51testing.com/attachments/2018/02/14982672_2018020611100619XYp.gif)](http://www.51testing.com/batch.download.php?aid=82378)

Newman gif

## 在Linux，Windows或Mac上开始使用

　　Newman建立在Node.js. 要运行Newman，请确保已安装Node.js。Node.js可以下载并安装 在Linux，Windows和Mac OSX上。

　　一旦安装了Node.js，Newman只是一个命令。从系统的全局npm命令安装Newman，让您从任何地方运行它。

　　$ npm install -g newman

　　运行Newman的最简单方法是使用集合来运行它。您可以从文件系统运行任何集合文件。请参阅 集合文档 ，了解如何导出集合以作为文件共享。

　　$ newman run mycollection.json

　　您也可以将一个集合作为URL传递。请参阅集合文件，了解如何以URL的形式共享文件。您的集合可能使用环境变量。要提供一组伴随的环境变量，请从Postman 导出模板，并使用该-e 标志运行它们。

　　$ newman run https://www.getpostman.com/collections/cb208e7e64056f5294e5 -e dev_environment.json

## 选项

　　纽曼提供了丰富的选项来自定义运行。可以通过使用该-h 标志来运行选项列表。
```
$ newman run -h
Options:
Utility:
-h, --help                      output usage information
-v, --version                   output the version number
Basic setup:
--folder [folderName]           Specify a single folder to run from a collection.
-e, --environment [file|URL]    Specify a Postman environment as a JSON [file]
-d, --data [file]               Specify a data file to use either json or csv
-g, --global [file]             Specify a Postman globals file as JSON [file]
-n, --iteration-count [number]  Define the number of iterations to run
Request options:
--delay-request [number]        Specify a delay (in ms) between requests [number]
--timeout-request [number]      Specify a request timeout (in ms) for a request
Misc.:
--bail                          Stops the runner when a test case fails
--silent                        Disable terminal output
--no-color                      Disable colored output
-k, --insecure                  Disable strict ssl
-x, --suppress-exit-code        Continue running tests even after a failure, but exit with code=0
--ignore-redirects              Disable automatic following of 3XX responses
```
　　使用该-n 选项设置运行集合的迭代次数。

　　$ newman run mycollection.json -n 10  # runs the collection 10 times

　　要提供不同的数据集，即每次迭代的变量，可以使用该数据-d 来指定JSON或CSV文件。例如，如下所示的数据文件将运行 2 次迭代，每次迭代使用一组变量。
```
[{
"url":"http://127.0.0.1:5000",
"user_id":"1",
"id":"1",
"token_id":"123123",
},
{
"url":"http://postman-echo.com",
"user_id":"2",
"id":"2",
"token_id":"899899",
}]
```
$newmanrunmycollection.json-ddata.json
　　上述变量组的CSV文件将如下所示：

　　url, user_id, id, token_id

　　http://127.0.0.1:5000, 1, 1, 123123123

　　http://postman-echo.com, 2, 2, 899899

　　默认情况下，Newman退出状态码为0，如果一切正常运行，即没有任何例外。持续集成工具可以对这些退出代码进行响应，并相应地通过或失败构建。您可以使用``-bail 标志告诉Newman停止[**测试**](javascript:;)用例错误，状态代码为1，然后可以由CI工具或构建系统进行选择。

　　$ newman run PostmanCollection.json -e environment.json --bail newman
　　示例集合与失败的测试
```
→ Status Code Test
GET https://echo.getpostman.com/status/404 [404 Not Found, 534B, 1551ms]
1\. response code is 200
┌─────────────────────────┬──────────┬──────────┐
│                         │ executed │   failed │
├─────────────────────────┼──────────┼──────────┤
│              iterations │        1 │        0 │
├─────────────────────────┼──────────┼──────────┤
│                requests │        1 │        0 │
├─────────────────────────┼──────────┼──────────┤
│            test-scripts │        1 │        0 │
├─────────────────────────┼──────────┼──────────┤
│      prerequest-scripts │        0 │        0 │
├─────────────────────────┼──────────┼──────────┤
│              assertions │        1 │        1 │
├─────────────────────────┴──────────┴──────────┤
│ total run duration: 1917ms                    │
├───────────────────────────────────────────────┤
│ total data received: 14B (approx)             │
├───────────────────────────────────────────────┤
│ average response time: 1411ms                 │
└───────────────────────────────────────────────┘
#  failure        detail
1\.  AssertionFai…  response code is 200
at assertion:1 in test-script
inside "Status Code Test" of "Example Collection with
Failing Tests"
```
　　所有测试和请求的结果可以导出到一个文件中，然后导入Postman进行进一步分析。使用JSON报告和一个文件名将流程输出保存到一个文件中。

　　$ newman run mycollection.json --reporters cli,json --reporter-json-export outputfile.json

　　注意： Newman允许您使用 Postman支持的所有 库和对象来运行测试和预请求脚本。

## 文件上传

　　Newman还支持文件上传。为了正常工作，要上传的文件必须放置在集合中指定的相对位置。例如，对于以下集合：
```
{
"variables": [],
"info": {
"name": "file-upload",
"_postman_id": "9dbfcf22-fdf4-f328-e440-95dbd8e4cfbb",
"description": "A set of `POST` requests to upload files as form data fields",
"schema": "https://schema.getpostman.com/json/collection/v2.0.0/collection.json"
},
"item": [
{
"name": "Form data upload",
"event": [
{
"listen": "test",
"script": {
"type": "text/javascript",
"exec": [
"var response = JSON.parse(responseBody).files[\"sample-file.txt\"];",
"",
"tests[\"Status code is 200\"] = responseCode.code === 200;",
"tests[\"File was uploaded correctly\"] = /^data:application\\/octet-stream;base64/.test(response);",
""
]
}
}
],
"request": {
"url": "https://echo.getpostman.com/post",
"method": "POST",
"header": [],
"body": {
"mode": "formdata",
"formdata": [
{
"key": "file",
"type": "file",
"enabled": true,
"src": "sample-file.txt"
}
]
},
"description": "Uploads a file as a form data field to `https://echo.getpostman.com/post` via a `POST` request."
},
"response": []
}
]
}
```
　　该文件sample-file.txt 必须存在于与集合相同的目录中。收集可以照常运行。

　　$ newman run file-upload.postman_collection.json

## 文档库**

　　Newman从一开始就建成了一个文档库，以便以各种方式进行扩展和使用。您可以在Node.js代码中使用它：
```
var newman = require('newman'); // require newman in your project
// call newman.run to pass `options` object and wait for callback
newman.run({
collection: require('./sample-collection.json'),
reporters: 'cli'
}, function (err) {
if (err) { throw err; }
console.log('collection run complete!');
});
```
　　定制报告
　　想要生成针对特定用例的集合运行报告，自定义报告将派上用场。例如，当请求（或它的测试）失败时输出响应日志，等等。

## 建立自定义报告

　　自定义报告是具有表单名称的Node模块newman-reporter-<name>。创建自定义报告：

　　1、导航到您选择的目录，并创建一个空白的npm软件包npm init。

　　2、添加一个index.js导出以下形式的函数的文件：
```
function (emitter, reporterOptions, collectionRunOptions) {
// emitter is is an event emitter that triggers the following events: https://github.com/postmanlabs/newman#newmanrunevents
// reporterOptions is an object of the reporter specific options. See usage examples below for more details.
// collectionRunOptions is an object of all the collection run options: https://github.com/postmanlabs/newman#newmanrunoptions-object--callback-function--run-eventemitter
};
```
　　3、发布您的报告使用npm publish，或使用您的报告本地查看使用说明。

　　有作用范围内的报告软件包名称例如@myorg/newman-reporter-<name>也被支持。使用报告的例子可以在使用报告的例子中找到。

　　使用自定义报告

　　为了使用自定义的报告，必须首先安装。例如，使用Newman的报告：

　　安装报告包。

　　npm install newman-reporter-teamcity

　　请注意，包的名称是形式newman-reporter-<name>，<name>是报告的实际名称。如果Newman全局安装，则本地安装应为全局，否则为局部安装。运行全局安装npm install ...的-g标志。

　　要使用本地（未发布）的报告，请运行该命令npm install <path/to/local-reporter-directory>。

　　通过CLI或通过编程方式使用已安装的报告。这里，newman-reporter在选项中指定报告名称时，不需要前缀。

　　有作用范围报告程序包必须用范围前缀指定。例如，如果你的包名是@myorg/newman-reporter-name，你必须指定记者@myorg/name。

　　CLI：

　　newman run /path/to/collection.json -r myreporter --reporter-myreporter-<option-name> <option-value> # The option is optional

　　编程方式：
```
var newman = require('newman');
newman.run({
collection: '/path/to/collection.json',
reporters: 'myreporter',
reporter: {
myreporter: {
'option-name': 'option-value' // this is optional
}
}
}, function (err, summary) {
if (err) { throw err; }
console.info('collection run complete!');
});
```
　　在上述两种情况下，报告选项是可选的。

　　有关详细信息的完整列表，请参阅 Newman README。