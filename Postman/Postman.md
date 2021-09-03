# 一. postman安装说明

​		postman 在 2018 年之后就不再支持浏览器版本，所以，想要使用它就必须先下载客户端再安装使用，下面就以 Windows 系统为例进行安装 。

## 下载与安装

​	postman安装步骤：

1. 访问postman官方网站，下载最新版本

   访问地址：https://www.getpostman.com/

2. 进入到下载页面，根据自己电脑下载对应的版本

   ![图片](Postman.assets/640.png)

3. 双击下载的安装包，进入到安装界面，直到用户登录和注册界面。

   若个人使用，选择跳过即可，这时会进入到postman主界面，至此postman安装成功(下图)。若团队使用，可以进行注册，注册后使用账号可以加入团队工作区。

   ![图片](Postman.assets/640-1617326534907.png)

## 界面导航说明

​		初次使用postman的朋友可能对界面上的一些元素不太熟悉，下面就通过一张图来说明这些元素的含义 。

![77d68338-1145-46fa-81f3-35e001626d42.png](Postman.assets/77d68338-1145-46fa-81f3-35e001626d42.png)

## 发送第一个请求

​		如果你是第一次使用postman发送请求，下面这个例子可以作为一个最基本的入门，可以帮我们建立一个初始印象 。

1. 打开postman，点击+加号打开一个新的请求页。
2. 在请求的URL中输入请求地址：http://www.weather.com.cn/data/sk/101010100.html
3. 点击Send按钮，这时就可以在下部的窗格中看到来自服务器的json响应数据。

![1b448a7c-85ab-4d1b-be83-c20d5e998861.png](Postman.assets/1b448a7c-85ab-4d1b-be83-c20d5e998861.png)

# 二.postman基础功能

## 常见类型的接口请求

​		常见的接口有如下四种类型，分别是含有查询参数的接口，表单类型的接口，json类型的接口以及含有上传文件的接口，以下就对这四种类型接口及如何在postman中请求进行说明 。

### 查询参数的接口请求

#### 什么是查询参数?

​		所谓的查询参数，其实就是URL地址中问号（?）后面的部分就叫查询参数，比如：http://cx.shouji.360.cn/phonearea.php?number=13012345678 。在这个接口中，查询参数就是:**number=13012345678** 。而这一部分是由有键值对组成，格式为：key1=value1&key2=value2, 如果有多组键值对，要用&隔开 。

#### postman如何请求

​		在postman中实现对这类接口请求非常简单，一般就需要明确俩个参数即可，一个是请求方法，一个请求地址。针对上面的那个接口，地址已经给出 ，而它的请求方法是get 。那么在postman中只需要把这俩个参数填写上即可请求 。

具体实现步骤：

1. 打开postman，新建一个请求。
2. 在请求方法中选择请求方法：GET,因为在postman中默认的请求方法就是GET,所以这一步可以忽略
3. 接口URL中输入地址，点击Send按钮就可以发送请求了 。

![ffd06d98-8877-4758-9b88-2ef3741010bc.png](Postman.assets/ffd06d98-8877-4758-9b88-2ef3741010bc.png)

​		说明：查询参数的URL一般直接拷贝到输入的URL地址栏中就可以了，当然也可以把查询参数在Params中输入，俩者的效果是一样的 。

### 表单类型的接口请求

#### 什么是表单 ？

​		我们都知道，在发送HTTP请求的时候，一个请求中一般包含三个部分，分别是请求行，请求头，请求体 。

​		不同的接口，请求体的数据类型是不一样的，比较常见的一种就是表单类型，那么什么是表单类型呢 ？简单理解就是在请求头中查看**Content-Type，它的值如果是:application/x-www-form-urlencoded** .那么就说明客户端提交的数据是以表单形式提交的 。见下图：

![eb1a7eea-8cee-4078-9a4c-ed2d2ae44933.png](Postman.assets/eb1a7eea-8cee-4078-9a4c-ed2d2ae44933.png)

#### postman中如何请求

​		如果在postman请求上图的接口，我们只需要填写四个参数，分别是(可以参考上图)：

- 请求方法：POST
- 请求URL：http://localhost/index.php?m=Home&c=User&a=do_login&t=0.21942974229794432
- 请求头：Content-Type：application/x-www-form-urlencode
- 请求体：username=13088888888&password=123456&verify_code=8888

​		实现步骤：

1. 打开postman，新建一个请求 。
2. 在请求中设置以上四个参数，点击Send按钮。在postman中设置请求体类型为，需要**选择body-> x-www-form-urlencoded**
3. 查看响应数据。

![73b75a3a-a96a-47e9-acce-287b6b33d5a5.png](Postman.assets/73b75a3a-a96a-47e9-acce-287b6b33d5a5.png)

### 上传文件的表单请求

#### 什么是上传文件？

​		在做接口测试时，我们经常会遇到需要上传文件的接口，比如微信的更新头像。这就需要用到：multipart/form-data。它也属于一种表单，但它既支持表单请求，也支持文件上传。它的请求报文中数据往往是下面这样的。

```shell
POST http://localhost/index.php/home/Uploadify/imageUp/savepath/head_pic/pictitle/banner/dir/images.html HTTP/1.1
Content-Type: multipart/form-data

file=a1.jpg
```

#### postman中如何请求

​		这种类型的接口，在postman中该如何请求呢 ？我们先分析需要填写的参数 。

- 请求方法：POST
- 请求URL：http://localhost/index.php/home/Uploadify/imageUp/savepath/head_pic/pictitle/banner/dir/images.html
- 请求类型：multipart/form-data
- 请求体：file=a1.jpg

​		实现步骤：

1. 打开postman，新建一个请求 。
2. 在请求中设置以上四个参数，点击Send按钮。注意：在postman中设置请求体类型，需要**选择body-> form-data** 。file中要选择File类型，然后上传本地的文件 。
3. 查看响应数据。

![2c888229-7970-4733-b39e-4ce07f19d604.png](Postman.assets/2c888229-7970-4733-b39e-4ce07f19d604.png)

### json类型的接口请求

#### 什么是json接口请求

​		这应该是接口测试中最常见的一种情况了 ， 也就是请求体类型为json,我们来看下这个请求报文 。

```shell
POST http://xxx/api/sys/login HTTP/1.1
Content-Type: application/json;charset=UTF-8

{"account":"root","password":"123456"}
```

#### postman中如何请求

​		根据以上报文，我们可以分析出，我们在postman只需要填写四个参数即可，具体如下：

- 请求方法：POST
- 请求地址：http://xxx/api/sys/login
- 请求体类型：json
- 请求体数据：{"account":"root","password":"123456"}

​		实现步骤：

1. 打开postman，新建一个请求 。
2. 在请求中设置以上四个参数，点击Send按钮。注意：在postman中设置请求体类型，需要**选择body-> raw -JSON**
3. 查看响应数据。

![54e33e61-5707-48f7-85b3-8702b02e80e7.png](Postman.assets/54e33e61-5707-48f7-85b3-8702b02e80e7.png)

## 接口响应数据解析

​		响应数据是发送请求后经过服务器处理后返回的结果，响应由三部分组成，分别是状态行、响应头、响应体。我们来看下postman的响应数据展示。

![c8726bcd-fd5d-436d-89e1-2ae641fb58e8.png](Postman.assets/c8726bcd-fd5d-436d-89e1-2ae641fb58e8.png)

​		在postman中的响应数据展示：

- 状态行：Status：200 OK
- 响应头：Headers + Cookies，需要注意的是Cookies是包含在响应头中的，但是为了明显，工具会分开显示
- 响应体：Body

​		那么这些数据对我们做接口测试有什么作用呢 ？

- Body和Status是我们做接口测试的重点，一般来说我们都会验证响应体中的数据和响应状态码
- Test Results 是我们编写断言后，可以查看断言的执行结果 ，所以这个对我们也很有用 。
- Time 和Size 是我们做性能测试时，可以根据这两个参数来对所测接口的性能做一个简单的判断。

​		接下来我们再来关注下Body中的几个显示主题，分别是：Pretty，Raw，Preview .

![img](Postman.assets/68330faf-5904-4be6-9d02-32e1cff5ff94.png)

​		**Pretty**:翻译成中文就是漂亮 ， 也就是说返回的Body数据在这个标签中查看 ，都是经过格式化的，格式化后的数据看起来更加直观，所以postman默认展示的也是这个选项。比如返回html页面，它会经过格式化成HTML格式后展示，比如返回json，那么也会格式化成json格式展示 。

​		**Raw**：翻译成中文未经过加工的，也就是原始数据 ，原始数据一般都是本文格式的，未经过格式化处理的，一般在抓包工具中都有这个选项 。

​		**Preview**：翻译成中文就是预览，这个选项一般对返回HTML的页面效果特别明显，如请求百度后返回结果，点击这个选项后就直接能查看到的页面 ，如下图 。同时这个选项和浏览器抓包中的Preview也是一样的 。

![bc1eabb7-44d4-4324-9222-bc6351c9024e.png](Postman.assets/bc1eabb7-44d4-4324-9222-bc6351c9024e.png)

## 接口管理（Collection）

​		当我们对一个或多个系统中的很多用例进行维护时，首先想到的就是对用例进行分类管理，同时还希望对这批用例做回归测试 。在postman也提供了这样一个功能，就是Collection 。通过这个Collection就可以满足我们的上面说的需求。

​		先对Collection功能的使用场景做个简单总结 。

- 用例分类管理，方便后期维护
- 可以进行批量用例回归测试 。

​		那么Collection是如何去管理用例的呢 ？先想象我们要测试一个系统，系统下有多个模块，每个模块下有很多的被测接口用例 。那么基于这个场景，我们来通过Collection来进行实现：

1. 点击Collection，点击+New Collection，在弹出的输入框中输入Collection名称（这个就可以理解为所测试的系统）

   ![e4e600d2-7890-40cc-840d-fd309be32623.jpg](Postman.assets/e4e600d2-7890-40cc-840d-fd309be32623.jpg)

2. 选中新建的Collection右键，点击Add Folder ，在弹出对话框中输入文件夹名称（这个就可以理解为系统中的模块）

   ![34b133bc-f6c9-44a4-a477-63f52b198ba5.jpg](Postman.assets/34b133bc-f6c9-44a4-a477-63f52b198ba5.jpg)

3. 选中新建的Folder，点击Add Request ，在弹出的对话框中输入请求名称，这个就是我们所测试的接口，也可以理解为测试用例 。

   ![8b24b95e-f5ab-4c9a-8a2d-7bdb05e908d1.jpg](Postman.assets/8b24b95e-f5ab-4c9a-8a2d-7bdb05e908d1.jpg)

   那么通过以上三个步骤，达到的效果就是如图所示：

   ![一文带你全面解析postman工具的使用（基础篇）](Postman.assets/c56094f4de8b46e78315f10505c904f2.jpg)

​		总结，通过上面的操作，我们实现了一个最简单的demo模型。但实际上，有了这个功能才是postman学习的开始，因为很多功能都是基础这个功能的基础上进行的，比如用例的批量执行，Mock ，接口文档等功能 。

## 批量执行接口请求

​		当我们在一个Collection中编写了很多的接口测试用例，想一起执行这批用例，在postman中是如何操作呢 ？

​		实现步骤：

1. 选中一个Collection，点击右三角，在弹出的界面点击RUN

   ​	![一文带你全面解析postman工具的使用（基础篇）](Postman.assets/e90ab1b7678847178b3ba5286968012f.png)

2. 这是会弹出一个叫Collection Runner的界面，默认会把Collection中的所有用例选中 。

   ![一文带你全面解析postman工具的使用（基础篇）](Postman.assets/4d0ce051479443b09ee98d83708a7bd4.png)

3. 点击界面下方的RUN Collection，就会对Collection中选中的所有测试用例运行 。

   ![一文带你全面解析postman工具的使用（基础篇）](Postman.assets/8a961d30f1e141418971592124ecfb3a.png)

   ​		对上面的几个红框内的功能进行简单说明：

   - **断言统计**：左上角的两个0是统计当前Collection中断言成功的执行数和失败的执行数，如果没有编写断言默认都为0 。
   - **Run Summary**: 运行结果总览，点击它可以看到每个请求中具体的测试断言详细信息 。Export Result：导出运行结果，默认导出的结果json文件 。
   - **Retry**: 重新运行，点击它会把该Collection重新运行一遍
   - **New**：返回到Runner，可以重新选择用例的组合 。

   ​		总体来说，这个功能主要是用于对一个Collection中的所有用例或部分用例进行批量运行，已达到手工回归测试的目的。

## 日志调试

​		在做接口测试时，经常会因为代码写的有问题导致报错，这时通过查看日志就显得非常重要了，postman也提供了这样的功能，它允许我们在脚本中编写打印语句，查看打印的结果 ; 同时也可以查看每个请求的日志信息 。

​		在postman中编写日志打印语句使用的是JavaScript，编写的位置可以是Pre-request Script 或Tests标签中。编写打印语句如：console.log("我是一条日志")

![一文带你全面解析postman工具的使用（基础篇）](Postman.assets/012c94ef73584406aa1dffd8eb9fd7af.png)

​		那么打印的日如何看呢 ？ 

​		第一个入口就是：view-show postman console 。

![一文带你全面解析postman工具的使用（基础篇）](Postman.assets/ef9de08de3fc4b0cb3b494138851c6c5.png)

​		第二个入口就是左下角第三个图标 。

![一文带你全面解析postman工具的使用（基础篇）](Postman.assets/e56b98ace56d40f8b1c14fd72458e1fe.png)

​		这里面有几个比较实用的功能：

- **搜索日志**：输入URL或者打印的日志就能直接搜索出我们想要的请求和日志，这对我们在众多日志中查找某一条日志是非常方便的 。
- **按级别搜索**：可以查询log,info,warning,error级别的日志 ，有助于我们更快定位到错误 。
- **查看原始报文(Show raw log)**：如果习惯看原始请求报文的话，这个功能可能更方便些 。
- **隐藏请求(Hide network)**：把请求都隐藏掉，只查看输出日志 。

​		总之，通过这个功能，我们在请求接口报错时，通过打印响应的日志，就能很轻松地找到问题原因了 。

## 断言

​		如果没有断言，我们只能做接口的功能测试，但有了断言后，就为我们做自动化提供了条件，并且在postman中的断言是非常方便和强大的 。

​		我们先来了解下postman断言的一些特点 ，具体如下

- 断言编写位置：Tests标签
- 断言所用语言：JavaScript
- 断言执行顺序：在响应体数据返回后执行 。
- 断言执行结果查看：Test Results

​		从上面介绍看到，编写的断言代码是JavaScript，那如果不会写怎么办 ？ 不用担心，因为postman已经给我们内置了一些常用的断言 。用的时候，只需从右侧点击其中一个断言，就会在文本框中自动生成对应断言代码块 。

![一文带你全面解析postman工具的使用（基础篇）](Postman.assets/8ada897ccaf144bdb2648deeffc262c5.png)

​		接下来就让我们了解一些常用断言，还是按响应的组成来划分，分别是状态行，响应头，响应体。

​		状态行中又包括状态码，状态消息 。在postman也可以对这两个进行断言。

### 状态行中的断言

#### 断言状态码

```javascript
//Status code: code is 200
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200); //这里填写的200是预期结果，实际结果是请求返回结果
});
```

#### 断言状态消息

```javascript
//Status code：code name has string
pm.test("Status code name has string", function () {
    pm.response.to.have.status("OK");   //断言响应状态消息包含OK
});
```

### 响应头中的断言

#### 断言响应头中包含

```javascript
//Response headers:Content-Type header check
pm.test("Content-Type is present", function () {
    pm.response.to.have.header("Content-Type"); //断言响应头存在"Content-Type"
});
```

### 断言响应体(重点)

#### 断言响应体中包含XXX字符串

```javascript
//Response body:Contains string
pm.test("Body matches string", function () {
    pm.expect(pm.response.text()).to.include("string_you_want_to_search");
});     
//注解
pm.expect(pm.response.text()).to.include("string")      获取响应文本中包含string
```

#### 断言响应体等于XXX字符串

```javascript
//Response body : is equal to a string
pm.test("Body is correct", function () {
    pm.response.to.have.body("response_body_string");
});
//注解
pm.response.to.have.body("response_body_string");   获取响应体等于response_body_string
```

#### 断言响应体(json)中某个键名对应的值

```javascript
//Response body : JSON value check
pm.test("Your test name", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.value).to.eql(100);
});
//注解
var jsonData = pm.response.json()// 获取响应体，以json显示，赋值给jsonData .注意：该响应体必须返会是的json，否则会报错
pm.expect(jsonData.value).to.eql(100)// 获取jsonData中键名为value的值，然后和100进行比较
```

### 响应时间(一般用于性能测试)

#### 断言响应时间

```javascript
//Response time is less than 200ms
pm.test("Response time is less than 200ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(200);   //断言响应时间<200ms
});
```

### 案例

​		针对以下接口返回的数据进行断言：

```json
{
    "cityid": "101120101",
    "city": "济南",
    "update_time": "2020-04-17 10:50",
    "wea": "晴",
    "wea_img": "qing",
    "tem": "16",
    "tem_day": "20",
    "tem_night": "9",
    "win": "东北风",
    "win_speed": "3级",
    "win_meter": "小于12km/h",
    "air": "113"
}
```

- 断言响应状态码为200
- 断言city等于济南
- 断言update_time包含2020-04-17

![一文带你全面解析postman工具的使用（基础篇）](Postman.assets/7c3a8a662d74414db265997d227a0e3c.png)

​		总结，整体来说，如果用postman做接口测试，这个断言功能必不可少，其中我们常断言的响应体包含和JSON这俩个断言又是重重之重。

## 变量（全局/集合/环境）

​		变量可以使我们在请求或脚本中存储和重复使用其值，通过将值保存在变量中，可以在集合，环境或请求中引用。对我们做接口测试来说，又是一个非常重要的功能 。

​		在postman常用的三种变量分别是全局变量，环境变量，集合变量 。

- **全局变量**：一旦申明了全局变量，全局有效，也就是说postman中的任何集合，任何请求中都可以使用这个变量。它的作用域是最大的 。
- **环境变量**：要申明环境变量，首先的创建环境，然后在环境中才能创建变量 。如果要想使用环境变量，必须先选择(导入)这个环境，这样就可以使用这个环境下的变量了 。需要说明的是环境也可以创建多个 。每个环境下又可以有多个变量 。
- **集合变量**：集合变量是针对集合的，也就是说申明的变量必须基于某个集合，它的使用范围也只是针对这个集合有效 。

​		其中，他们的作用域范围依次从大到小：全局变量>集合变量>环境变量 。 当在几个不同的范围内都申明了相同的变量时，则会优先使用范围最小的变量使。

​		想要使用变量中的值只需俩个步骤，分别是定义变量和获取变量 。

1. 定义变量（设置变量）
2. 获取变量（访问变量）

### 定义变量

​		定义全局变量和环境变量，点击右上角的小齿轮，弹出如下界面，就可以根据需求定义全局变量或者环境变量了。

![一文带你全面解析postman工具的使用（基础篇）](Postman.assets/45991db700494bd8a5224326f83ea1b1.png)

​		已经定义的全局变量和环境变量，可以进行快速查看。

![一文带你全面解析postman工具的使用（基础篇）](Postman.assets/4c33ca75e40d4bdb9eb15f2c76e3c2ea.png)

### 定义集合变量

​		选择一个集合，打开查看更多动作(**...**)菜单，然后点击编辑 。选择“变量”选项卡以编辑或添加到集合变量。

![一文带你全面解析postman工具的使用（基础篇）](Postman.assets/fd9012e6b04440ed88cff56ad363943f.jpg)

​		定义变量除了以上方式，还有另外一种方式 。但是这种方式在不同的位置定义，编写不一样。

​		在URL，Params , Authorization , Headers , Body中定义：

1. 1. 手工方式创建一个空的变量名
   2. 在以上的位置把想要的值选中右击，选中Set：环境|全局 ，选中一个变量名，点击后就会保存到这个变量中

![一文带你全面解析postman工具的使用（基础篇）](Postman.assets/a847339ed12a441e8512b3868bcbbcd2.png)

​		在Tests，Pre-requests Script：

- 定义全局变量：pm.collectionVariables.set("变量名",变量值)
- 定义环境变量：pm.environment.set("变量名"，变量值)
- 定义集合变量：pm.variables.set("变量名",变量值)

### 获取变量

​		定义好变量，接下来就可以使用变量了 。需要注意的是，在不同的位置获取变量，编写的规则也是不一样的。

​		如果在**请求参数中**获取变量，无论是获取全局变量，还是环境变量，还是集合变量，获取的方式都是一样的编写规则：{{变量名}} 。

- 请求参数指的是：URL，Params , Authorization , Headers , Body

​		如果是在编写代码的位置(Tests,Pre-requests Script)获取变量，获取不同类型的变量，编写的代码都不相同，具体如下：

- 获取环境变量：pm.environment.get(‘变量名’)
- 获取全局变量：pm.globals.get('变量名')
- 获取集合变量：pm.pm.collectionVariables.get.get('变量名')

![一文带你全面解析postman工具的使用（基础篇）](Postman.assets/623a4d170d5c437f84bde2384c8191c5.png)

​		变量的使用场景非常广泛，比如我们后面要提到的接口关联，请求前置脚本都会使用到变量 。

## 请求前置脚本

​		前置脚本其实就是在Pre-requests Script中编写的JavaScript脚本，想要了解这个功能，需要先了解它的执行顺序。那么下面就来看下它的执行顺序 。

​		可以看出，一个请求在发送之前，会先去执行Pre Request Script（前置脚本）中的代码 。那么这个功能在实际工作中有什么作用呢 ？

​		主要场景：一般情况下，在发送请求前需要对接口的数据做进一步处理，就都可以使用这个功能，比如说，登录接口的密码，在发送前需要做加密处理，那么就可以在前置脚本中做加密处理，再比如说，有的接口的输入参数有一些随机数，每请求一次接口参数值都会发送变化，就可以在前置脚本中编写生成随机数的代码 。总体来说，就是在请求接口之前对我们的请求数据进行进一步加工处理的都可以使用前置脚本这个功能。

​		接下来通过一个案例来看下该功能是如何使用 ？

### 案例

- 请求的登录接口URL，参数t的值要求的规则是每次请求都必须是一个随机数。
- 接口地址：http://localhost/index.php?m=Home&c=User&a=do_login&t=0.7102045930338428

![一文带你全面解析postman工具的使用（基础篇）](Postman.assets/3602cd49c9cd447ba44704855f169e2c.png)

​		实现步骤：

1. 在前置脚本中编写生成随机数
2. 将这个值保存成环境变量
3. 将参数t的值替换成环境变量的值 。

![一文带你全面解析postman工具的使用（基础篇）](Postman.assets/e44fc6b0ddf5431bbf779835611147e8.png)

​		总之，这个前置脚本对我们做接口测试也非常有用，对一些复杂的场景，都可以使用前置脚本进行处理后再请求接口 。

## 接口关联

​		在我们测试的接口中，经常出现这种情况 。 上一个接口的返回数据是下一个接口的输入参数 ，那么这俩个接口就产生了关联。 这种关联在做接口测试时非常常见，那么在postman中，如何实现这种关联关系呢 ？

​		实现思路：

1. 提取上一个接口的返回数据值，
2. 将这个数据值保存到环境变量或全局变量中
3. 在下一个接口获取环境变量或全局变量

### 案例

- 用户上传头像功能，需要用户先上传一张图片，然后会自动预览 。那么在这个过程中，会调用到俩个接口 ，第一个上传头像接口，第二个预览图像接口 。
- 其中调用上传头像接口成功后会返回如下信息：

```json
{
    "url": "/public/upload/user//head_pic//ba51d1c2f7f7b98dfb5cad90846e2d79.jpg",
    "title": "banner",
    "original": "",
    "state": "SUCCESS",
    "path": "images"
}
```

​		而图像预览接口URL为：http://localhost/public/upload/user//head_pic//ba51d1c2f7f7b98dfb5cad90846e2d79.jpg 。可以看出这个接口的URL后半部分其实是上一个接口返回的url的值 。那么这俩个接口就产生了关联。那么在postman 可以通过以下三步完成这俩个接口的关联实现 。

实现步骤：

1. 获取上传头像接口返回url的值
2. 将这个值保存成全局变量(环境变量也可以)
3. 在图像预览中使用全局变量

![一文带你全面解析postman工具的使用（基础篇）](Postman.assets/0dbe0d6e02344ffaae72a35a6dcb9e26.png)

​		可以看出，接口的关联的解决方案都是用的是变量中的知识，也就是说只要你明确了要提取的值，后面就是保存该值，然后在其他接口使用该值就可以了。

## 常见返回值获取

​		在做接口测试时，请求接口返回的数据都是很复杂的json数据，有着多层嵌套，这样的数据层级在postman怎么获取呢 ？

​		案例1：多层json嵌套, 获取user_id的值

```json
{
    "code": 0,
    "message": "请求成功！",
    "data": {
        "user_id": "1252163151781167104"
    }
}
```

```javascript
//获取json体数据
var jsonData = pm.response.json()
// 获取user_id的值,通过.获取
var user_id = jsonData.data.user_id
```

​		案例2：json中存在列表，获取points中的第二个元素

```json
{
    "code": 0,
    "message": "请求成功！",
    "data": {
        "roles": {
            "api": [
                "API-USER-DELETE"
            ],
            "points": [
                "point-user-delete",
                "POINT-USER-UPDATE",
                "POINT-USER-ADD"
            ]
        },
        "authCache": null
    }
}
```

```javascript
//获取json体数据
var jsonData = pm.response.json()
// 获取user_id的值,通过下标获取列表中某个元素
var user_id = jsonData.data.roles.points[1]
```

​		案例3：列表中取最后一个元素

```json
{
    "code": 0,
    "message": "请求成功！",
    "data": {
        "total": 24,
        "rows": [
           
            {
                "id": "1066370498633486336",
                "mobile": "15812340003",
                "username": "zbz"
            },
            {
                "id": "1071632760222810112",
                "mobile": "16612094236",
                "username": "llx"
            },
            ...
            {
                "id": "1075383133106425856",
                "mobile": "13523679872",
                "username": "test001",
       
            }
    }
}
```

```javascript
//获取json体数据
var jsonData = pm.response.json()
// 获取id的值,通过slice(-1)获取列表中最后一个元素。
var id = jsonData.data.rows.slice(-1)[0]
```

# 三、postman快捷功能

## 快速填写查询参数

​		查询参数在上面已经介绍过，在这里我们只说明postman填写查询参数的地方就是Params。

![一文带你全面解析postman工具的使用（效率篇）](Postman.assets/921ef1828fd4453480e54f8e49625b0a.png)

​		有时候我们要填写的参数比较多，且每个参数都是按照key-value形式填写完成，但是这样填写起来费时费力。那是否有更加省事的填写方式？ 答案肯定是有的 ，我们可以想象我们的这些请求都可以通过浏览器或抓包工具抓取到 。那么我们就可以直接将浏览器或抓包工具的请求参数直接拷贝进来 ，下面就介绍如何从浏览器和抓包工具中拷贝参数。

### 从浏览器拷贝查询参数

1. 首先在浏览器通过F12找到你要抓取的请求

2. 在Headers的最下端找到Form Data .

   ![一文带你全面解析postman工具的使用（效率篇）](Postman.assets/c9b7eb947a0a43a08d4cf4f6e5046494.png)

3. 然后打开postman，在Params 中点击Bulk Edit

   ![一文带你全面解析postman工具的使用（效率篇）](Postman.assets/3ed257925cbd4aba913779c0f40344e7.png)

4. 直接将拷贝的内容粘贴进来即可

![一文带你全面解析postman工具的使用（效率篇）](Postman.assets/9a2fe24cb65e49c58b33adca98d11ec7.png)

### 从抓包工具中拷贝查询参数(以fiddler为例)

1. 打开Fiddler，找到你要抓取的数据包

2. 选择Raw，直接拷贝请求URL或者拷贝查询参数

   ![一文带你全面解析postman工具的使用（效率篇）](Postman.assets/0607f99234d24be39a2e633a64fa08d9.png)

3. 直接粘贴到地址栏或者查询参数中即可 。

## 快速填写请求头

​		在我们做接口测试时，几乎每个接口都要填写headers，而且headers里的参数多是公共参数，也就是说每个接口都需要填写这些一样的参数 。常规操作也是在每个headers中按照key-value形式逐个填写完成，但是这样填写起来费时费力。接下来就介绍三种快捷设置headers 。

### 从其它请求拷贝粘贴

​		若我们要在一个headers中填写几个参数，而这些参数都已在其它请求的headers中设置过，那么这时就可以直接从其它请求中拷贝，具体操作步骤：

1. 进入已设置过的请求headers中，鼠标长按选择一个或多个请求，当出现灰色的横条，按Ctrl+C 。
2. 回到当前要设置的请求中，点击Ctrl+v .这样就会把上一个请求中的headers拷贝到当前请求 。

![一文带你全面解析postman工具的使用（效率篇）](Postman.assets/b4032e24d4f141218ea7f92559387c85.png)

​		通过如上设置，是否可以更加快捷地设置我们请求头了 。当然，觉得上面这种方法使用起来不爽，接下来我们来看另外一种快捷设置方法 。

### 预置(保存)公共请求

​		这个方法同样是对一些公共参数有效的，如果每个请求都要设置这些参数，那这个方法很有效。具体步骤：

1. 点击Headers选项框中的Presets（最右侧），点击Manage Presets .
2. 在弹出的对话框，点击Add。
3. 在弹出的对话框中，把常用的key-value录入，并给它起个名字。点击add即可。
4. 其他请求使用的时候，直接点击Presets ，选择刚才设置的名字，就会自动把对应的参数设置上 。

![一文带你全面解析postman工具的使用（效率篇）](Postman.assets/faa46cce180c4939a9f6426ce9e8d3d0.png)

​		以上的这两种方法设置起来虽然便捷，但是只是对公共参数有效。针对每个请求的唯一参数是无效的 。下面的这种方法是可以针对任何参数的 。

### 从浏览器中或者抓包工具中拷贝

​		在浏览器中拷贝或者从抓包工具拷贝跟上面的Params中的操作是一样的，这里就不再赘述了。

## 快速实现添加一个请求

​		正常情况下，我们添加一个请求需要打开一个窗口，选择请求方法，地址，以及相对应的参数 。如果请求过多，难免会觉得添加起来麻烦，那么在postman给我们提供一个导入功能，它可以导入相关的请求 。比较常用的是如下这三种，分别是：

- 从抓包工具中导入请求 ;
- 从浏览器中导入请求 ；
- 直接导入别人postman中写好的请求 。

![一文带你全面解析postman工具的使用（效率篇）](Postman.assets/3c846d757b774d4eb1907831b54da6ed.png)

### 从抓包工具导入请求

1. 在浏览器中抓取到想要的包，然后右键copy出Curl的数据包

   ![一文带你全面解析postman工具的使用（效率篇）](Postman.assets/f686394d685b4e0b8d6699f1681c0afd.png)

2. 在postman的import中将数据粘贴进来，就会自动生成了对应的请求 。

   ![一文带你全面解析postman工具的使用（效率篇）](Postman.assets/a958a61dcf9749019cc37ec88ba80b15.png)

​		下面的这个截图是从接口文档swagger，将这个数据包拷贝粘贴到上面的文本中(Paste Raw Text) 也可以自动生成请求 。

![一文带你全面解析postman工具的使用（效率篇）](Postman.assets/f14a0799b94c4db798d5f87e085cd75b.png)

​		总之，这个功能非常实用，尤其是可以把浏览器或抓包工具中的数据包导入进来直接使用，大大地减少了我们的接口填写时间 。

### 从浏览器中导入请求

​		从浏览器中导包的原理和抓包工具是一样的，以下为导入请求的步骤：

1. 在浏览器中抓取到想要的包，然后右键copy出Curl的数据包

   ![一文带你全面解析postman工具的使用（效率篇）](Postman.assets/821f6ae432c849e8b80d50e0226f0202.png)

2. 在postman的import中将数据粘贴进来，就会自动生成了对应的请求 。

   ![一文带你全面解析postman工具的使用（效率篇）](Postman.assets/d9005b895aee4ffdb04c0583e33b90b9.jpg)

### 直接导入别人postman中写好的请求 。

​		很多情况下，我们是每个人负责一部分的，当你用到其它同事写好的请求时，你就可以通过如下这个操作来完成，但是这个功能需要团队成员都登录postman账号。具体的操作步骤为：

1. 将已经写好请求所在的集合，点击分享

   ![一文带你全面解析postman工具的使用（效率篇）](Postman.assets/bf8677a094e346c483804028ed3e53b3.png)

2. 在弹出的界面点击Get public link

   ![一文带你全面解析postman工具的使用（效率篇）](Postman.assets/14ec4d5b923440098a29b0b7eda2feff.png)

3. 复制生成的链接

   ![一文带你全面解析postman工具的使用（效率篇）](Postman.assets/fa0c272269c441309557e53abe7af089.png)

4. 在新的postman账号中，选择Import-Import From Link 进行导入

   ![一文带你全面解析postman工具的使用（效率篇）](Postman.assets/3ca0378da635429093eefef50d9379e2.jpg)

   这样我们其它团队成员就可以通过这个功能共享写好的整个集合了 。

## 继承集合认证

​		这又是一个非常实用的功能，对我们做接口测试来说，经常要处理登录认证的情况 。如果不用这个Authorization其实也能解决认证的问题，无非就是把要认证的数据按照要求在指定位置传入参数即可。比如我们之前测试的系统，登录后返回的token要在每个请求接口的headers中传入 。这时就需要在每个headers中都填写一个认证参数传入 ，但是这样做的话太过繁琐，如果使用认证(Authorization)功能的话，就会大大简化了我们的认证过程。

​		我们先来看下这个功能的具体位置及主要作用 。

![一文带你全面解析postman工具的使用（效率篇）](Postman.assets/b05ad41970ed46d1a8f990a2701b77a7.png)

​		**Inherit auto from parent**:从父级继承身份验证，是每个请求的默认选择 。这是一个很有用的功能，当我们对一个集合(collection)进行测试的时候，集合中的每个请求都需要获取token，那么如果我们在集合中把token处理好的话，那么该集合下的所有请求都会自动获取到这个token，也就省略了我们对每个token进行处理了。

​		实现步骤：

1. 选中一个集合进行编辑，切换到Pre-Request Script.在这里请求登录接口 ，将返回的token值拿到，然后保存成全局变量 。
2. 切换到Authorization选项卡，在这里直接获取token 。这里的获取token需要根据具体的项目 。比如我们所测试的项目正好是Bearer token这种形式 。直接在列表中使用这种方式输入{{token}}即可。
3. 向集合添加请求，无需进行token处理，所有接口都能请求成功 。

![一文带你全面解析postman工具的使用（效率篇）](Postman.assets/7e7ac9952d814bcd860e74829ce82928.jpg)

![一文带你全面解析postman工具的使用（效率篇）](Postman.assets/240cac74076543e09cc64f5db44ef56f.png)

![一文带你全面解析postman工具的使用（效率篇）](Postman.assets/c029641b0f484270a3694311b8770699.png)

​		**No Auth**: 无需身份认证的可以选择这个 。

​		**API Key**: 也有很多系统是通过这种认证方式，比如在请求头添加 model: data xxx-xxx-xxx-xxxx

![一文带你全面解析postman工具的使用（效率篇）](Postman.assets/3c55104a52004831ac683417dbcb9c08.png)

​		**Bearer Token**:很多系统都是以这种认证方式，就是在请求头中添加Authorization：Bearer Token 。那么使用这种认证就完全等同于在Headers中添加Authorization参数 。

![一文带你全面解析postman工具的使用（效率篇）](Postman.assets/e2d9b631e6d84da9a5f1ba32429a4e95.png)

### 通过在集合中完成登录认证

​		除了以上访问完成登录认证以外，我们还可以在集合中完成登录认证 ，但是这个功能需要先熟悉如何通过实现发送请求，接收响应数据等 。

​		代码中发送请求是通过pm.sendRequest来完成的 。在Pre-requests Script 和Tests中都可使用 。支持发送各种类型的请求。具体如下：

- 代码中发送查询参数的请求数据
- 代码中发送JSON参数的请求数据
- 代码中发送表单参数的请求数据

#### 发送查询参数请求数据

```javascript
//发送一个get请求，请求成功后设置一个环境变量
pm.sendRequest('http://cx.shouji.360.cn/phonearea.php?number=13012345678', function (err, res) {
    if (err) {
        console.log(err);
    } else {
        pm.environment.set("xab", "123");
    }
});
```

#### 发送JSON请求数据

```javascript
const PostJsonRequest = {
  url: 'http://test.itheima.net/api/sys/login',
  method: 'POST',
  header: 'Content-Type:application/json',
  body: {
    mode: 'raw',
    raw: JSON.stringify({ "mobile": '13110001002',"password":"123456" })
  }
};
pm.sendRequest(PostJsonRequest, function (err, res) {
  console.log(err ? err : res.json());
});
```

#### 发送表单数据

```javascript
const PostFormRequest = {
  url: 'http://localhost/index.php?m=Home&c=User&a=do_login&t=0.8975232623499945',
  method: 'POST',
  header: 'Content-Type:application/x-www-form-urlencoded',
  body: {
    mode: 'x-www-form-urlencoded',
    raw: 'username=13088888888&password=123456&verify_code=8888'
  }
};
pm.sendRequest(PostJsonRequest, function (err, res) {
  console.log(err ? err : res.json());
});
```

​		以上代码都是可以放在Tests或者放在Pre-requests Script中使用的，那么通过它我们也可以解决登录认证的问题，以下通过一个案例来说明如何使用。

#### 案例

​		项目的token通过sendRequest来实现 。

​		实现步骤：

1. 点击集合右击，选择edit，切换到Pre-request Scripts中 .
2. 在文本域编写发送登录接口的前置脚本，并将获取到的token保存到集合变量 。
3. 然后在Authorization中设置获取token，使其token在集合中全局有效 。
4. 运行该集合（集合下就不需要编写登录请求了），批量运行成功 。

![一文带你全面解析postman工具的使用（效率篇）](Postman.assets/033287291c6e4715b1218f7982c2b2d9.png)

​		通过这种方式来设置，就不需要你在集合下面单独新建一个登录的文件夹了，也不需要你在每个请求中加入token参数了，非常的方便 。

## 批量断言

​		前面我们介绍过断言，就是对每个接口编写一个或多个验证点 ，在编写断言的过程中还有这么一种场景，就是多个接口中有部分接口返回的参数名都是一样的 ，包括返回的结果也是一样的 。那么针对这些返回相同的参数值来说，其实就可以使用一个共同的断言 。通过编写一个断言完成对不同接口中相同返回参数的批量断言 。比如说每个接口都会有code，或者HTTP的响应状态码都可以使用这个通用断言 。

​		编写通用断言的位置是在集合或集合的文件夹中 。具体位置如下图：

![一文带你全面解析postman工具的使用（效率篇）](Postman.assets/1cc2035178874257b3995df524b10955.png)

### 案例

​		对项目中每个接口返回的响应状态码进行断言，同时对用户管理模块下每个接口的code进行断言。

​		实现步骤：

1. 选择其中一个集合，进行编辑，选择Tests标签，在文本域内输入断言响应状态码的代码块
2. 选择用户管理文件夹，进行编辑，选择Tests标签，
3. 批量运行该集合，就会查看到每个用例中都会

![一文带你全面解析postman工具的使用（效率篇）](Postman.assets/e1df8e7f0efa4dd08dd513b27e5bf178.png)

![一文带你全面解析postman工具的使用（效率篇）](Postman.assets/9ebb6384255f409699b040a18ebf1ed6.png)

![一文带你全面解析postman工具的使用（效率篇）](Postman.assets/7ce6b9950858424e97df3b08c073edf3.png)

​		可以看出，通过这个功能可以帮我们完成最少的代码，完成更多的测试。但是它的使用条件就是返回的参数名，参数值都是一样的才能使用这个批量断言功能 。

## 快速查询与替换

​		有时候我们常会遇到这样一种问题，系统中有太多的用例，环境变量和系统变量的值也太多，查找其中的某个值太不方便；或者有的值想要修改，但苦于修改的地方太多，修改起来太费劲。那么，针对这样的困扰，是否有办法解决呢 ？ 答案是有的 ，那就是快速查询与批量替换。

​		接下来我们先来了解这个功能的入口和简单介绍。

![一文带你全面解析postman工具的使用（效率篇）](Postman.assets/8dc34eae9b0941be99da6527d06f9a90.png)

**功能介绍：**

- **FIND**:搜索输入框，在搜索框中输入你想要搜索的值，postman自动会在已打开的请求，集合，环境变量，全局变量中去搜索，如果搜索到，就会在右侧展示出搜素的结果 。其下方有两个复选框，分别是Regex(正则匹配)和Ignore Case(忽略大小写)。
- **WHERE**:带条件查询，默认会选择everything（查询所有），如果想要选择某一个tab搜索，从下面选择即可，可以支持从集合、环境变量、全局变量以及以打开的请求中搜索 。
- **REPLACE WITH**: 替换文本框，在此文本框中输入替换的值，点击Replace in ... 按钮，会将搜索出的值全部替换 。
- **右侧的搜索结果**：搜索出对应的结果后，右侧每个tab中都会显示具体的数字，代表当前tab中匹配值的数量。你可以选择一个值点击Open，就会直接进入到对应的功能选项卡中 。

### 案例

​		案例1：按照正则表达式搜索11位数字。

​		操作步骤：在搜索框中输入\d{11}，勾选Regex,点击Find，右侧就会展示出含有11位数字的所有信息。

![一文带你全面解析postman工具的使用（效率篇）](Postman.assets/13267461eca2480d99de88f0fb1c506c.png)

​		案例2：从集合中搜索

1. 在搜索框中输入搜索关键字
2. 在WHERE中选择Choose entities to find in，选中Collections 。
3. 找到你想要的结果，点击Open in builder。就可以直接打开对应请求tab.

![一文带你全面解析postman工具的使用（效率篇）](Postman.assets/eb24dd184e4a40bb8305c97a465a9f55.png)

​		案例3：替换某个字符串

1. 在查找搜索框中输入关键字，
2. 在REPLACE WITH框中输入想要替换的值，可以选择select All ,点击后面的按钮。
3. 再次搜索替换后的结果，发现所有值都已被替换 。

![一文带你全面解析postman工具的使用（效率篇）](Postman.assets/3fc1ccad1aa54c6d885674a664fb3a1d.png)

​		总之，通过这个功能，我们可以快速找到我们想要的集合，环境变量，集合变量，请求或者代码块。

# 四. 高级功能介绍

## 读取文件进行参数化

​		测试过程中，常会遇到一个接口要验证很多的测试数据，而输入参数又都是一样的。这时我们首先就会想到数据参数化（数据驱动），在postman中也提供了数据参数化功能，它需要把数据单独的存放在一个文件中管理，然后通过读取这个文件实现所有的数据的验证。

​		实现步骤 。

1. 在本地电脑创建数据文件，支持数据格式文件分别为csv和json 。在文件中分别包括参数名和数据
2. 其中，在postman中需要读取外部文件的参数名，通过参数名来获取文件中的数据；其中在不同的位置读取方式不同：在URL输入框，Params,Authorization,Headers,Body中读取数据方式为:{{参数名}}。在Pre-request Script和Tests中读取数据方式为:data.参数名
3. 通过Runner-Data读取数据文件来运行。

### 案例

​		请求天气接口，输入不同的城市id，会返回不同的城市和天气情况 ，需对返回城市和天气进行验证 。

1. 创建city.json 或 city.json ,格式如下

   ![一文带你全面解析postman工具的使用（高级篇）](Postman.assets/857878137d6a4031b9dbf1ca7eba40b9.png)

2. 在请求中替换参数名：city_id,city,weather .

   其中city_id在URL中替换，故通过{{}}替换 。

   city和weather在Tests中替换，需要通过data.city , data.weather

   ![一文带你全面解析postman工具的使用（高级篇）](Postman.assets/9a70ba57c9724c8f9b6ad96555ed2ccc.png)

3. 选择数据文件导入

   ![一文带你全面解析postman工具的使用（高级篇）](Postman.assets/8460f9cca87d4800805012d348e66ac3.jpg)

4. 查询运行结果

   ![一文带你全面解析postman工具的使用（高级篇）](Postman.assets/303cfcc8a4bf406f894dc56ea8a8a4cb.png)

## 生成测试报告

​		postman生成测试报告需要一个插件：newman ，并且这个插件需要先安装 。

​		**安装步骤：**

1. 安装nodejs: newman是由nodejs开发，所以要先安装它的运行环境，下载地址：http://nodejs.cn/download/ 。安装成功后需要验证：在cmd窗口中输入node -v,如果输出node的版本信息，则证明安装成功。
2. 安装newman：安装成功nodejs后，会自动安装一个包管理工具npm(类似于python中的pip)。通过它就可以直接安装newman。 打开cmd窗口输入：npm install -g newman .安装成功后进行验证：newman -v 。如果输出newman的版本信息，则证明安装成功 。
3. 安装newman-reporter-html:通过这个插件可以指定报告的生成路径和名称。同样打开cmd窗口输入：npm install -g newman-reporter-html.安装成功后进行验证：npm list -g --depth 0.如果能出现newman-reporter-html包及版本及证明安装成功 。

​		通过newman生成测试报告必须在cmd执行，命令执行：newman run <collection> [options] ，其中options中有很多参数，接下来我们来解析下这些参数。

​		**命令解析：**

- -e : 可选，指定一个URL或者postman的环境变量脚本文件。如果集合中指定了环境变量，则需要添加这个参数。

- -g：可选，指定一个URL或者postman的全局变量脚本文件，如果集合中指定了全局变量，则需要加这个参数 。

- -r：可选，指定测试报告的类型，如果想生成对应的报告类型，需要添加这个参数，典型的有html,json,cli，若不添加，默认为cli。

- -d：可选，指定一个数据参数化文件 ，如果有参数化文件，需要添加这个选项。

- --reporter-html-export：可选，指定生成报告的路径和文件名，如果不添加该参数，默认会生成一个newman的文件夹，里面存放着生成的测试报告

  输入的命令就可以是下面这样的 。

  ```shell
  newman run collect_a.json [-e environment_b.json] [-r html] [--reporter-html-export report.html]  其中[]内的参数是可选的。
  ```
### 案例

  ​		案例1：通过newman生成测试报告，集合为一个URL。

  ```shell
命令：
newman run https://www.getpostman.com/collections/6e95413b91fe582ec78d  说明：run后面跟的链接可以通过分享得到
  ```

​		案例2：通过newman生成测试报告，报告格式为默认:cli

```shell
newman run A.postman_collection.json  -r cli //默认的展示结果如下图所示。
```

![一文带你全面解析postman工具的使用（高级篇）](Postman.assets/871c22b86e3b431d8e06b8178a3c07e0.png)

​		案例3：通过newman生成测试报告，需要添加环境变量文件，并且生成HTML报告 。

```shell
newman run B.postman_collection.json -e test.postman_environment.json -r html
```

​		案例4：通过newman生成测试报告，需要制定报告路径和文件名称。

```shell
newman run B.postman_collection.json -e test.postman_environment.json -r html --reporter-html-export report.html   //生成的测试报告会存放在当前路径下，报告名为：report.html
```

### 更漂亮的报告

​		安装插件：newman-reporter-htmlextra

​		打开cmd窗口，输入命令：npm install -g newman-reporter-htmlextra

​		验证安装：npm list -g --depth 0

​		生成报告：

```shell
newman run APITest.postman_collection.json -r htmlextra --reporter-html-export htmlReport.html
```

![一文带你全面解析postman工具的使用（高级篇）](Postman.assets/6b866d3411d248c4bda01df914a6b524.gif)

​		虽然newman提供了强大的生成测试报告功能，但是目前为止，生成的测试报告都是在我们本地，那如果想要把报告展示给团队成员查看呢 ？ 我们就可以通过jenkins进行持续集成，把生成的报告展示在Jenkins上，甚至可以将报告通过邮件发送给团队成员 。

## 使用工作空间

​		前面我们说集合(Collection)就像一个项目，通过建立一个集合，可以对其集合中的用例进行分类管理；当然如果有多个项目，也可以建多个而项目进行管理。而接下来要学习的工作空间更是对不同集合进行分类管理，比如说我要新建一个自己学习的工作空间，也可以新建一个用于工作的工作空间。这样就可以在不同的工作空间内管理不同的集合，达到集合的有效管理 。

​		接下来看下工作空间的主要功能介绍：

- 将元素添加到另外一个工作空间
- 邀请成员加入工作空间
- 将集合和环境共享到工作空间
- 查看工作空间的详细信息
- 重命名工作区
- 离开工作区
- 编辑工作区的描述
- 管理团队工作区的成员

### 将元素添加到另外一个工作空间

​		你可以将集合或环境从一个工作空间添加到另一个工作空间。这样就使得数据在不同的工作空间内进行共享 。

​		实现步骤：

1. 点击postman导航栏中间的工作空间(下三角)，选择All workspaces .

   ![一文带你全面解析postman工具的使用（高级篇）](Postman.assets/7edd939c08774ef6b90a2f311503d018.png)

2. 在弹出的页面中，选择一个工作空间，点击Add to workspace.（向这个工作空间共享数据）

   ![一文带你全面解析postman工具的使用（高级篇）](Postman.assets/712a3d64cb2a4fe99ffca318e3a02a0a.png)

   - 当然除了添加到工作空间数据外，你也可以进行重命名，进行查看详情，添加成员以及删除工作空间 。具体操作点击Add to workspace后的(...)
   - 你可以将添加后的元素从工作空间删除，就是右击集合，点击‘Remove to workspace’，点击后从工作区中删除

3. 选择一个要共享的工作空间，选择集合或环境，点击Add to this workspace

   ![一文带你全面解析postman工具的使用（高级篇）](Postman.assets/9ff4cb941e9d43c98e88e39403c4423d.png)

   ![一文带你全面解析postman工具的使用（高级篇）](Postman.assets/f573d59ce6fa4d06921d32ec235481fa.png)

### 邀请成员加入工作空间

​		一个团队的工作空间，往往需要多个团队成员来共同维护，这时如果想往工作空间中加入新成员，就需要通过下面的邀请成员到工作区，具体如下：

​		实现步骤：

1. 点击postman导航栏中间的Invite.在弹出的对话输入框输入邮箱地址(邮箱一定要和账号绑定)，点击Add 。
2. 添加到文本域后，给账号设置角色，点击Send Invitarions 。
3. 进入邮箱点击链接验证，验证成功后即可成员该空间的成员 。同时会自动将该空间的集合同步到本地 。备注：除了以上可添加成员后，也可以通过工作空间后的...，选择Add Members 也可以添加成员。

![一文带你全面解析postman工具的使用（高级篇）](Postman.assets/1171dd48b08f46bbbaafa8a40b3c75bf.jpg)

### 将集合和环境共享到工作空间

​		有时候，我们需要把在本地的集合或环境分享给团队的工作空间中，这样团队其他成员就都可以看到并使用了。

​		共享集合到工作空间

1. 选择一个集合，点击（...）或者右键，点击Share Collection .
2. 在弹出的界面中，选择要共享的工作空间，点击Share and Continue .
3. 这样该集合就会被该工作空间的所有成员看到并有权限操作，当然上面也可以选择共享给工作空间中部分成员。

![一文带你全面解析postman工具的使用（高级篇）](Postman.assets/1d74644e4acd4f2bb0a6952e65b73443.png)

## 集合的分支管理

​		像git一样，在postman中也有源码管理功能，通过创建团队的workspace，团队成员可以在这个workspace中像git管理源代码一样，创建分支，合并分支，拉取分支等。创建workspace见XXX 。

​		接下来我们就先来了解下postman的这几个功能 。

- 创建集合分支（Create a fork）
- 合并变更（Merge changes）
- 创建pull请求（Create Pull Request）

### 创建集合分支

​		分支的创建，需要基于某个集合中，集合分支创建后， 这就相当于这个集合的主分支，团队成员可以基于这个分支拉取一个新的分支开发，最后将修改的新的脚本合并到主分支上。接下来是创建一个分支：

1. 选中一个集合，点击(...)或右键，点击“Create a fork”
2. 在弹出的对话框中输入Fork Label ，选择团队的workspace ，点击“Fork collection” 。
3. 进入到对应的workspace，就会查看到对应的collection ,这里的集合后都有一个fork的标志。

![一文带你全面解析postman工具的使用（高级篇）](Postman.assets/7c1a2c5ccd974561b318d7e4748f98ae.png)

### 合并变更

​		当我们在集合中加了新的功能后，我们就需要把这些变更提交到主分支上，提交成功后，团队成员也能看到你最新的修改数据了，那么如何进行合并操作呢？

1. 点击Collection右侧的（...），点击Merge Changes.
2. 在弹出的页面中，点击右上角的Merge all changes .注意，这时merge时提示已经有最新更新了，postman会提示你pull Changes，这时你可以先拉取最新的变更 ，然后点击 Merge all changes。
3. 在弹出的新对话框默认选择Merge changes，点击Merge 。

![一文带你全面解析postman工具的使用（高级篇）](Postman.assets/70a6d464af6345098b45ec75fe7a71e6.png)

![一文带你全面解析postman工具的使用（高级篇）](Postman.assets/e21bdca0bb874867b4f978b0c3cc9180.jpg)

### 创建 Pull 请求

​		当团队提交了最新修改后，我们就可以通过Create pull Request拉取最新的修改数据 。

​		操作步骤：

1. 点击Collection右侧的（...），点击Create pull Request.
2. 在弹出的页面中，输入title和描述，点击 Create pull Request .
3. 查看postman请求，最新的更新就会拉取到本地的分支集合中 。

![一文带你全面解析postman工具的使用（高级篇）](Postman.assets/28bcc8b079d74f268b67f179dfb0f834.png)

​		在使用的过程中，postman中的Create a fork ,Create pull request, Merge change 就特别像git中的create branch ，pull ，push 。

## 编写接口文档

​		在做接口测试时，经常会出现填写的请求数据不太清楚，这时我们首先会想到的就是接口文档 。但很多时候开发写的文档也不是很完善，更新并不及时 ；亦或是更新了，我们也得跳出工具去找对应的接口文档，用户体验上不太好。所以，现在出现了一些工具既支持接口调试也同时支持文档的查看，无需在工具和文档之间来回切换 。那么在postman中也是支持编写接口文档的 ，而且它的文档功能还非常强大 。

​		接下来我们介绍postman跟接口文档的相关功能 。

- 生成文档(链接)
- 编写文档

### 生成文档

​		生成文档有两种方式，直接打开链接和新建API文档。

​		第一种：直接打开链接非常简单，就是选择一个集合，点击右三角,点击View in web 。

​		第二种，操作步骤如下：

1. 点击左上角的New，选择API Documentation .
2. 弹出的第一个Tab页面有两个选项，是新建一个集合还是从已有集合选择 。根据自己的需求来选择。
3. 进入到第二个Tab页面，输入对集合的一些基本描述 ，比如基本介绍，认证方式，错误码等 。
4. 进入到第三个Tab页面，这时会弹出一个链接，直接点击链接就会进入到接口文档页面 。如下图

![一文带你全面解析postman工具的使用（高级篇）](Postman.assets/1d17ea2e9fd14a7daa9e3211acd7bfa0.png)

​		以上两个都可以进入文档链接，主要区别在于第二种可以加入一些整体性的说明，如系统概况，认证方式，错误码等 。

​		另外文档是以web形式展现，所以只要有人知道这个链接，就都可以在浏览器访问 。

### 编写文档

​		编写文档同样有两种方式，分别是在本地编辑，或者打开链接在浏览器中编辑 。无论哪种方式，保存成功后都会自动同步，也就是所有人都能看到 。

​		**本地编辑步骤：**

1. 点击集合的右三角，会自动弹出RUN的窗口

2. 选择一个请求点击后，会出现两个链接按钮，分别是Add a description和Open in builder 。

3. 点击Add a description，这这里就可以填写接口描述。

   **在线编辑步骤：**

4. 点击集合的右三角，会自动弹出RUN的窗口

5. 点击View in web，会在浏览器中自动打开该集合的web链接地址。

6. 选择其中请求，点击Add a description .

​		以上两种方式都可以给接口添加文档描述，且都支持**markdown**语法，编写好的信息也能及时的文档中看到，如下图是给其中一个接口添加的文档信息 。

![一文带你全面解析postman工具的使用（高级篇）](Postman.assets/18bbb8abf7f84141b92d7b849daf69db.jpg)

​		同时点击Open in builder这个链接按钮，也能直接打开对应的请求 。

​		以下是打开的web在线文档，在线文档还有个比较实用的功能，就是为每个请求自动生成不同语言的代码，如果你正好对如何用代码实现不太清楚，那么你就可以直接从这里拷贝

![一文带你全面解析postman工具的使用（高级篇）](Postman.assets/fb98d55750d64cf0b3163c4f09e8780c.png)

![一文带你全面解析postman工具的使用（高级篇）](Postman.assets/ba6f0a4f0d364b63ac985d743320090e.png)

## Mock服务

### 什么是Mock服务 ？

​		正常情况下，前端需要调用后端的接口才能完成一个完整的功能实现，但由于后端接口交付的延迟，严重影响了工作效率，这时为了减少对后端接口的依赖，前端开发人员创建一个mock服务器，以模拟每个请求对应的响应。开发人员更加模拟响应进行接口调试，而无需增加后端 。在postman中也支持创建mock服务器。

### 创建mock服务器

​		在postman中最常见创建mock服务的两种方式：在运行面板中创建和通过new窗口创建 。

​		**new窗口创建步骤**：

1. 点击左上角的New，选择弹出的窗口选择Mock Server。
2. 需要为即将要创建的Mock Server , 可以从已有的选择，也可以重新创建一个集合 。
3. 选择对应的mock名称，版本标签，环境等，点击Create Mock Server 。

![一文带你全面解析postman工具的使用（高级篇）](Postman.assets/8893316186c8426da00f27bfec4de227.gif)

​		**面板中创建**

1. 选择集合，点击右三角，在弹出的面板中选择Mocks,点击Create a mock Server.
2. 在弹出的界面中输入mock server name ,version tag , environment,点击Create mock server 。完成创建

​		

​		以上两种方式创建，最终结果都会在mock标签中生成一个mock服务器的链接，具体如下：

![一文带你全面解析postman工具的使用（高级篇）](Postman.assets/4e3e1fe941c0471c8c68a817e6e68529.png)

### 创建mock请求

​		上文我们提到过，接口若不能准时提供给前端人员，我们就需要模拟对应的接口，但是模拟接口前，我们先要确定好接口的请求方法，请求路径，返回状态码，以及响应数据 。至于请求传递的参数我们无需关注 。所以无论通过何种工具去模拟，至少以上几个参数 。

​		那么通过postman模拟请求，就需要用到example.接下来我们就来了解下如何通过example模拟请求 。

​		**example功能入口**：

![一文带你全面解析postman工具的使用（高级篇）](Postman.assets/aee47c8631544c3ab50f33193b0ca0dd.png)

通过example实现模拟请求步骤：

1. 选择一个请求，通过发送请求后，点击Save Response中的Save as example。
2. 这时会自动弹出一个tab页，打开的这个页面其实就是postman的example.也是我们要说的模拟请求 .
3. 在弹出的example页面，需要将请求方法，请求路径，响应状态码及相应数据填写好 ，点击右上角的Save Example。
4. 保存成功后，就会在右上角能看到我们要保存的example了 。
5. 以上步骤相当于创建好了一个模拟请求了，接下来我们就可以通过工具请求这个example(模拟请求)了 。在postman打开一个新的tab页，请求方法填写保存好的example的方法，**请求地址要填写mock服务器地址+请求路径**，点击Send.就会将预期结果返回 。

![一文带你全面解析postman工具的使用（高级篇）](Postman.assets/29d7e87a3a4f4cbb8617e711f4bdc73d.png)

## 监控

​		postman的监控，和Jenkins中设置的定时任务差不多，用于监控接口的运行情况和性能 。同样的这个功能用于集合。你可以配置多长时间运行一次，到了时间点将自动遍历集合中的每个请求。那么很明显通过这个功能，真正地帮我们实现了自动化 。

### 创建监视器

​		同样的创建监视器有两种方法，分别是通过new创建和面板中创建 。 接下来就主要介绍下面板创建的步骤

​		**面板创建实现步骤**

1. 选择集合，点击右三角，弹出的面板中选择Monitors,点击Create a monitor
2. 在Configuration中配置环境，定时任务，运行地区，以及设置其他偏好，点击Create后即创建了监控。

![一文带你全面解析postman工具的使用（高级篇）](Postman.assets/2b1bd69981334a75bb96b769c944a121.png)

![一文带你全面解析postman工具的使用（高级篇）](Postman.assets/dbf2da5025044845b1898676b6165a3c.png)

### 查看监视器

​		创建好的监视器，就是通过编辑查看监视器中运行的数据 。

![一文带你全面解析postman工具的使用（高级篇）](Postman.assets/e00dfcce7aed45139d5ab118f68fd52a.png)

## 连接数据库

​		对于做接口测试，其中很重要的一个环节就是要连接数据库 ， 那么对于我们使用的postman而言，是否也可以进行连库操作呢 ？ 答案是肯定的 。这里就需要到一个插件:xmysql.

​		通过xmysql连库后，xmysql会将数据库中所有表以REST风格的接口形式生成 ，所以后续访问某张表其实就是访问的某个接口，那么对于postman而言，其实也就是相当于访问了某个接口而已。

### 安装

1. 安装nodejs: xmysql是由nodejs开发，所以要先安装它的运行环境，下载地址：http://nodejs.cn/download/ 。安装成功后需要验证：在cmd窗口中输入node -v,如果输出node的版本信息，则证明安装成功。
2. 安装xmysql：安装成功nodejs后，会自动安装一个包管理工具npm(类似于python中的pip)。通过它就可以直接安装xmysql。 打开cmd窗口输入：npm install -g xmysql.

### 连接数据库

​		xmysql命令参数介绍：

```shell
-h  连接数据库主机名
-u  连接数据库用户名
-p  连接数据库密码
-d  连接数据库名
-r  连接数据库输入的主机名，无这个选项默认为localhost
-n  连接这个服务设置的端口，无这个选项默认为3000
```

​		举例:

```shell
> xmysql -u username -p password -d databasename
```

​		连接本地数据库的示例，注意输入这条命令后，xmysql会以服务的形式启动 。所以当xmysql被停止掉，那么连库操作也会失败 。

![一文带你全面解析postman工具的使用（高级篇）](Postman.assets/5046cb5117dc4f3aa25c2f1da9fb3609.png)

### 数据库的基本操作

​		以下是我其中一张表t_book的数据，我们通过xmysql来对这张表分别进行增，删，改，查 。再次强调，无论何种操作，在postman中只是请求的是接口 。

![一文带你全面解析postman工具的使用（高级篇）](Postman.assets/4c40c958dd49456f9cbf22238c6b1263.png)

​		**需求1：查询t_book表的所有数据。**

```shell
GET http://localhost:3000/api/t_book
```

![一文带你全面解析postman工具的使用（高级篇）](Postman.assets/8efce5a052b6490e8752853e593b0f33.png)

​		**需求2：查询t_book表title为三国演义的数据。**

```shell
GET http://localhost:3000/api/t_book?_where=(title,eq,三国演义)
```

​		**需求3：向t_book表插入一条数据**

​		插入数据需要先知道表结构，t_book的表结构如下图，那么向这张表插入数据，其实就是将这些字段作为参数输入即可 。它支持两种请求，表单和json都可以请求

![一文带你全面解析postman工具的使用（高级篇）](Postman.assets/1263af5709c54199bbfd7b5920d4802a.png)

​		postman中是这样请求的，如果是修改数据直接把POST修改成PUT就可以了。

![一文带你全面解析postman工具的使用（高级篇）](Postman.assets/955b964d2c914484939946ae744d650f.jpg)

​		**需求4：删除其中一条数据。**

```shell
DELETE http://localhost:3000/api/t_book/5   //5是表中的ID值
```

### xmysql用法

#### 关系表

​		xmysql自动识别外键关系并提供GET API。

```shell
/api/blogs/103/comments
```

​		例如：blogs是父表，comments是子表。API调用将产生blogs主键103的所有注释。

#### 分页

​		**p和_size**

​		p表示页面，*size表示每页的数据量

​		默认情况下，每个GET请求在一个表上返回20条记录，最多返回100条记录。

```shell
/api/payments?_size=50
/api/payments?_p=2
/api/payments?_p=2&_size=50
```

​		当_size大于100时-记录数默认为100（即最大）

​		当_size小于或等于0时-记录数默认为20（即最小值）

#### 排序

##### **ASC（升序）**

```shell
/api/payments?_sort=column1
```

​		例如：按column1升序排序

##### **降序**

```shell
/api/payments?_sort=-column1
```

​		例如：按column1降序排序

##### **多个字段排序**

```shell
/api/payments?_sort=column1,-column2
```

​		例如：按column1升序排序，按column2降序排序

##### 列过滤/字段

```shell
/api/payments?_fields=customerNumber,checkNumber
```

​		例如：在每条记录的响应中仅获取customerNumber和checkNumber

```shell
/api/payments?_fields=-checkNumber
```

​		例如：获取表行中的所有字段，但不获取checkNumber

#### 运算符

##### **比较运算符**

```shell
eq      -   '='         -  (colName,eq,colValue)
ne      -   '!='        -  (colName,ne,colValue)
gt      -   '>'         -  (colName,gt,colValue)
gte     -   '>='        -  (colName,gte,colValue)
lt      -   '<'         -  (colName,lt,colValue)
lte     -   '<='        -  (colName,lte,colValue)
is      -   'is'        -  (colName,is,true/false/null)
in      -   'in'        -  (colName,in,val1,val2,val3,val4)
bw      -   'between'   -  (colName,bw,val1,val2) 
like    -   'like'      -  (colName,like,~name)   note: use ~ in place of % 
nlike   -   'not like'  -  (colName,nlike,~name)  note: use ~ in place of %
```

​		**使用比较运算符**

```shell
/api/payments?_where=(checkNumber,eq,JM555205)~or((amount,gt,200)~and(amount,lt,2000))
```

##### 逻辑运算符

```shell
~or     -   'or'
~and    -   'and'
~xor    -   'xor'
```

​		**使用逻辑运算符**

​		例如：简单的逻辑表达式

```shell
/api/payments?_where=(checkNumber,eq,JM555205)~or(checkNumber,eq,OM314933)
```

​		例如：复杂的逻辑表达式

```shell
/api/payments?_where=((checkNumber,eq,JM555205)~or(checkNumber,eq,OM314933))~and(amount,gt,100)
```

​		例如：具有排序（*sort），分页（*p），列过滤（_fields）的逻辑表达式

```shell
/api/payments?_where=(amount,gte,1000)&_sort=-amount&p=2&_fields=customerNumber
```

​		例如：使用_where的行过滤器也可用于关系路由URL。

```shell
/api/offices/1/employees?_where=(jobTitle,eq,Sales%20Rep)
```

##### 查找一条数据

```shell
/api/tableName/findOne?_where=(id,eq,1)
```

​		与list相似，但仅返回前一个结果。与_where结合使用 

##### 计数

```shell
/api/tableName/count
```

​		返回表中的行数 

##### 判断是否存在

```shell
/api/tableName/1/exists
```

​		根据记录是否存在返回真或假 

##### 按查询参数分组

```shell
/api/offices?_groupby=country
```

​		例如：选择国家/地区，从办事处按国家/地区计数（*）

```shell
/api/offices?_groupby=country&_having=(_count,gt,1)
```

​		例如：SELECT country，count（1）as _count FROM office GROUP BY country_count> 1

##### 以API分组

```shell
/api/offices/groupby?_fields=country
```

​		例如：选择国家/地区，从办事处按国家/地区计数（*）

```shell
/api/offices/groupby?_fields=country,city
```

​		例如：从办事处选择国家，城市，计数（*）GROUP BY国家，城市

```shell
/api/offices/groupby?_fields=country,city&_having=(_count,gt,1)
```

​		例如：SELECT country，city，count（*）as _count FROM office GROUP BY country_city _count> 1

##### 分组依据，排序依据

```shell
/api/offices/groupby?_fields=country,city&_sort=city
```

​		例如：通过办事处选择国家，城市，数量（*），按国家，城市分组，按城市ASC

```shell
/api/offices/groupby?_fields=country,city&_sort=city,country
```

​		例如：从办事处选择国家，城市，数量（*）按国家分组，按城市ASC订购，国家ASC

```shell
/api/offices/groupby?_fields=country,city&_sort=city,-country
```

​		例如：从办事处选择国家，城市，计数（*）按国家分组，城市按城市ASC，国家DESC。