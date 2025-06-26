---
title: php+mysql+ajax学习
date: 2019-03-23 16:48:53
tags:
- php
- MySQL
categories:
- php
- MySQL
---
- PHP是用于网页服务器端编程的脚本语言。WEB服务器是安装了WEB服务器软件的计算机，存储网站脚本程序

- 用户请求对应脚本时，服务器执行对应的脚本并返回执行结果

### - 搭建 WEB 服务器（提供网站服务的机器）

### - 服务端开发（动态网页技术）

### - HTTP（浏览器与服务端的通讯协议）

### - 数据库操作（服务端存储数据方式）

- AJAX（浏览器与服务端的数据交互方式）

- 服务器（提供服务）指的就是一台安装特定的软件的计算机，用于专门用于提供特定的服务。

- 按照服务类型的不同，又划分为：Web 服务器、数据库服务器、文件服务器等等。

- 客户端（使用服务）指的是在一次服务过程中使用这个服务的设备（网络端点）。

- 目前咱们最常见的客户端就是浏览器

 

## IP 地址

设备在某一个网络中的地址，目前最常见的格式：`[0-255].[0-255].[0-255].[0-255]` 即为四个 `0-255` 的数字组成。 `192.168.83.77`

作用就是标识一个网络设备（计算机、手机、电视）在**某一个具体的网络**当中的地址。

`127.0.0.1` 是本地回环地址 localhost：用来测试本机服务器是否连通

 

## 域名

由于 IP 地址都是没有规律的一些数字组成的，很难被人记住，不利于广泛传播，所以就有人想出来要给 IP 起名字（别名）。

 

## 特殊的域名

localhost 含义为本地主机，对应`127.0.0.1` 。这是一个保留域名，主要用于本地测试。

#### **顶级域名（了解）**

.com: 商业机构 .cn: 中国国家、地区域名 .hk,.gov: 政府网站。.org: 机构。.edu: 教育网站。.net: 网络服务商。 php.net.mil: 军事。

### **DNS**

通过宽带运营商提供的服务器解析一个域名背后对应的 IP，这个过程叫做 **DNS 寻址**，帮你完成 DNS 寻址过程的服务器叫做 **DNS 服务器**。

#### **hosts 文件**

操作系统在发起对 DNS 服务器的查询请求之前，会优先检查本机的 hosts 文件。如果这个文件中包含了对当前需要解析的域名的配置，则不再发起对 DNS 服务器的请求，直接使用 hosts 文件中的配置。

**文件所在路径：**

Windows：`C:\Windows\System32\drivers\etc\hosts`

macOS：`/etc/hosts`

注意：

本机的 `hosts` 文件配置只能到影响本机的 DNS 寻址

只有以管理员权限运行的编辑器才有权利修改 hosts 文件

### **端口**

计算机本身是一个封闭的环境，就像是一个大楼，如果需要有数据通信往来，必须有门，这个门在术语中就叫端口，每一个端口都有一个编号，每台计算机只有 65536 个端口（0-65535）。

一般我们把“占门”的过程叫做监听

可以通过在命令行中运行： <font color="#f0f">netstat -an</font> 命令监视本机端口使用情况：

![img](https://qq292383147.github.io/pictureLibrary/picture/php_mysql_ajax/1.png) 

- http 默认的端口 80

- https 默认的端口是 443</br>

## <font face="Brush Script Std" size="8">URL</font>

<font color="#f0f">**URL（Uniform Resource Locator）**</font>，统一资源定位符，通俗点来说就是表示网络当中某一个网页的完整访问地址，它具有一定的格式：


协议名称://域名:端口/文件目录(文件名称)?key=value&key2=value2


<h1> 请求响应流程 (重要)</h1>

1. 用户打开浏览器

2. 地址栏输入我们需要访问的网站网址（URL）

3. 浏览器通过  DNS 服务器 获取即将访问的网站  IP 地址

4. 浏览器发起一个对这个 IP地址的 请求

5. 服务端中   监听指定的 端口 的服务器软件   接收到这个请求，进行相应的处理

6. 服务端将处理完的结果返回给客户端浏览器（响应）

7. 浏览器将服务端返回的结果呈现到界面上

 

**Web 服务器软件分类（了解）**

- Nginx

<font color="#f0f">- Apache  -  php</font>

- IIS  -  C#    .net

- Tomcat  -   java

 

## 配置第一个虚拟主机

 

- 单击“其它选项菜单” 》 “站点域名管理",在弹出的对话框中 设置 ”站点域名“，”目录“，”第二域名“，”端口“，之后单击”新增“，同时单击”保存设置并添加到配置文件“

- 配置hosts文件，在这个文件中添加当前的域名映射。单击”其它选项菜单“>"打开host"

- 如果当前目录下没有默认可执行文件，那么就会报错，如果想展示目录结构，就需要通过修改配置文件的方式来实现。”其它选项菜单“>”打开配置文件">"vhots-ini"  :Options Indexes FollowSymLinks ExecCGI

- 重启服务器(通过phpstudy面板进行的设置 ，服务器会自动的重启，但是如果手动的设置修改了配置文件，那么就需要手动的重启服务器)

 

## 配置第二个虚拟主机

 

- 单击“其它选项菜单” 》 “站点域名管理",在弹出的对话框中 设置 ”站点域名“，”目录“，”第二域名“，”端口“，之后单击”新增“，同时单击”保存设置并添加到配置文件。

- 产生了新的问题：它会重新的生成配置文件内容并写入，会将之前对day1.com的配置重新覆盖，造成无法展示目录结构--重新添加Indexes,并重启服务器

- 配置hosts文件，在这个文件中添加当前的域名映射。单击”其它选项菜单“>"打开host"

 

## Apache 与 PHP

 

对于很多初学者来说，很容易把 Apache 和 PHP 混在一起 混为一谈，其实他们两者各自有各自负责的领域，各自的职责，但是我们在使用 PHP 做动态网站开发时，两者就会产生联系，具体如下：

 

Apache 是根据文件的扩展名找到文件的类型，然后挨个问一下每一个模块能否处理这个类型的文件，如果这些模块都不能处理，那么 Apache 就自己处理（按照静态文件的方式处理）



![img](https://qq292383147.github.io/pictureLibrary/picture/php_mysql_ajax/2.png) 

 

## php语言的特点

- <font color="#f0f">开源（open source）</font>软件，跨平台，常用操作系统稳定执行。Windows / Linux。做WEB开发的经典组合 WAMP,LAMP基本都是开源软件。

- 入门简单,用户只需要关注应用，开发成本低。

- 支持的大多数主流数据库。`MySQL`，`oracle,Redis`等

- 存在大量针对PHP开发的框架。如Laravel,ThinkPHP,Yii,CoderIgniter,Symfony等，加快开发速度

## PHP 标记

```php
<?php 可以让代码进入“PHP 模式”
  
?> 可以让代码退出“PHP 模式”
```

  

 

### 输出内容的方式

​    <font color="#ffe090">echo</font>:输出多个字符串

​    <font color="#ffe090">print</font>:输出一个字符串值

​    <font color="#ffe090">print_r</font>:可以输出复杂数据类型，如数组，以键值对的形式输出

​    <font color="#ffe090">var_dump</font>:可以输出复杂数据类型，如数组，以键值对的形式输出，还可以输出数据的长度

## 变量

> 1. 变量是编程语言中临时存放数据的容器。
> 2. PHP 中申明一个变量是用一个美元符号后面跟变量名来表示。变量名同样是区分大小写的。
> 3. PHP 中变量无需声明类型，变量的类型根据值的类型来推断。

### 变量的生命周期

> 1. 全局变量：声明的时候产生，页面执行完毕后销毁
> 2. 局部变量：函数执行的时候产生，函数执行完毕销毁。

可以通过unset()手动销毁变量。

## 静态变量

> 1. 静态变量放在函数内部
> 2. 作用域不变，还是在函数的内部访问，但是生命周期变了，页面执行完毕后才销毁。
> 3. 静态变量只能被初始化一次。

 

 

## 定义常量

><font color="#98e165">1. 定义常量使用的是内置的 `define` 函数</font>
><font color="#98e165">2. 第一个参数是常量的名称，建议采用全大写字母命名，多个单词下划线分隔</font>
><font color="#98e165">3. 第二个参数是常量中存放的数据，可以是任意类型</font>
><font color="#98e165">4. 第三个参数是常量名称是否区不分大小写，默认 false 区分大小写</font>

eg:define('SYSTEM_NAME', '阿里百秀');

## 使用常量

<font color="#98e165">1. 直接通过常量的名称访问常量</font>

<font color="#98e165">2. 与变量不同的是不需要用 $</font>

```php
echo SYSTEM_NAME;

echo SYSTEM_ENABLE;
```

## 常用函数

>1. isset(): 判断变量是否定义了，同时它还可以判断变量的值是否为 `null`,如果定义了且值不为null,则返回 `true`,否则返回 `false`
>2. empty(): 判断变量是否为空值，为空的值有：""  0 "0", null, false, array().如果值为以上中的某一个，则返回 `true` 值
>3. unset(): 删除变量

   - 如果删除一个变量，那么变量的值会置为 null

   - 可以同时删除多个变量

   - 如果在函数中删除全局变量，那么并不会真正的将全局变量删除

 

## 数据类型

- string（字符串） 

- integer（整型）—— 只能存整数

- float（浮点型）—— 可以存带小数位的数字

- boolean（布尔型）

- array（数组） 

- object（对象）

- NULL（空）

### 数据类型的分类：

- 基本数据类型：`string`（字符串） `integer`（整型） `float`（浮点型） `boolean`（布尔型）

- 复合数据类型： `array`（数组） `object`（对象）

- 特殊数据类型：`NULL`（空） 资源

### 判断数据类型：

`is_string()`: 判断当前变量是否是字符串类型

`is_bool()`: 判断当前变量是否是布尔类型

`is_int()`: 判断当前变量是否是整形类型

`is_float()`: 判断当前变量是否是浮点类型

`is_array()`: 判断当前变量是否是数组类型

`is_object()`: 判断当前变量是否是对象类型

### 字符串（重要）

PHP 有多种创建字符串的方式：单引号、双引号等。

### 单引号字符串

不支持特殊的转义符号，例如 \n

如果要表示一个单引号字符内容，可以通过 \' 表达

如果要表示一个反斜线字符内容，可以通过 \\ 表达

### 双引号字符串

```php
支持转义符号：\"  \  $  \r \n \t

支持变量解析
```

 

### 数组（重要）

PHP有混合数组的概念：说明数组中的成员是索引数组和关联数组成员的混合

如果没有手动设置key，那么 `key` 由系统自动生成.索引值是根据数组中最后一个索引值 +1

如果手动设置 `key`，那么这个 `key` 也不会影响系统自动生成的索引值

 

Strlen本质上不能获取宽字符串集的长度，所谓宽字符集就是指PHP默认不支持的字符(中文等等...)

它并不能获取这些宽字符串的长度，所以在调用这个函数的时候，会根据这些字符所占据的[字节数]来获取长度值

Gb2312:一个中文占 2 个字节

Utf8：一个中文占 3 个字节

它可以获取指定字符串的长度，但是它需要确定引入了一个扩展 `php_mbstring.dll`

通过 php.ini 进行配置：extension = php_mbstring.dll

 

## PHP 中数组

索引数组（用户只是存入数据，索引由系统自动生成）

  与 JavaScript 中的数组基本一致

 关联数组（用户自定义key和value）

 深度数组（数组中的每一个元素又是一个数组）

```php
array(
	Array(
		Key =>value
	)
)
```

 

1. ## 获取数组长度

<font color="#98e165">count()</font>

<font color="#98e165">sizeof()</font>

 

### 文件引入

<font color="#98e165">require</font>

<font color="#98e165">require_once</font>

<font color="#98e165">include</font>

<font color="#98e165">include_once</font>

 

`include` 一般用于载入公共文件，这个文件的存在与否不能影响程序后面的运行

`require` 用于载入不可缺失的文件

至于是否采用一次载入（once）这种方式取决于被载入的文件

 

## 文件包含

include:如果**载入失败**，**不会**报错，后续代码会继续**执行**，它可以重复**载入**

require:如果**载入失败**，**会**报错，后续代码**不**会继续**执行**，它可以重复**载入**

 

include_once:如果**载入失败**，**不会**报错，后续代码会继续**执行**，它不会重复载入，**只会**真正的载入一次

require_once:如果载**入失败**，会报错，后续代码**不**会继续**执行**，它**不**可以重复**载入**

 

 

<font color="red">注意：如果想在函数内部使用，则可以通过关键字global</font>

Global:引用全局变量。通过global关键字可以实现在**函数内部**使用函数外部声明的成员

不能再引用全局变量同时赋值，如果想赋值，那么换一行赋值

如果在函数内部修改了全局成员的值，这个值真正的被修改了.

 

## PHP的API

 

### 时间处理

Asia/Shanghai  - 上海

Asia/Chongqing  - 重庆

Asia/Hong_Kong  - 香港

修改配置文件：php.ini data.timezone：Asia/Shanghai

 

文件操作

File_get_contents()  将文件读入字符串 **可以读取文件内容并返回**

File_put_contents(文件路径，写入的内容，FILE_APPEND)  **将字符串写入文件 可以将指定的字符串内容写入到文件，其中第三个参数FILE_APPEND可以实现文件内容的追加**

 

函数的声明和使用：

1. 声明

```php
function 函数名称（参数）{

//函数体

return 返回值

}
```



2. 使用：通过函数名称调用

3. 细节:  函数内部默认不能直接使用函数外部声明的成员，如果想使用，可以：

Global:引入全局变量

$GLOABALS：所有全局成员都在这个数组中，在整个php文件都能使用

 

**拆分字符：explode(拆分元素(字符),字符串); //返回数组**

foreach

作用：用来遍历数组

语法1：

foreach(数组 as 值){}

语法2：

foreach(数组 <font color="pink">**as**</font> 键 <font color="pink">**=>**</font>值){}

想创建通用代码，让程序自动获取到当前文件的路径

$SERVER[‘PHP_SELF’]就可以自动的获取当前文件的路径

```php
<form action="<?php echo $_SERVER['PHP_SELF'] ?>"method='get'>
```

<font color="#0d9">Get方式 - - - $_GET</font>

<font color="#0d9">Post方式 - - -$_POST</font>

### $_REQUEST:可以接受任意类型请求方式所传递的参数

### <font color="#023">它可以接收get、post、cookie、session的参数，它有一个接收参数的排序规则，如果key名重名，那么后面接收的参数会将前面的数据覆盖--所以它不安全</font>

 

### 表单基本使用

```php
HTML中有一个专门提交数据的标签<form>,通过这个标签可以容易的收集用户输入

Form标签有两个必要属性：

Action：表单提交地址

Method：表单以什么方式提交
```

 

### PHP中有三个超全局变量专门用来获取表单提交内容：

```php
$_GET:用于获取以GET方式提交的内容（接收URL地址问号参数中的数据）

$_POST:用于获取以POST方式提交的内容（接收请求体中的数据）

$_REQUEST:用于获取GET或者POST方式提交的内容
```

 

![img](https://qq292383147.github.io/pictureLibrary/picture/php_mysql_ajax/3.png) 

 

判断是否是 post 请求

理论上说，`get` 和  `post` 上传文件的大小是没有限制，但是服务器对其做了限制

如果向修改这个设置，则需要找到配置文件 php.ini 进行相关配置

```php
if($_SERVER['REQUEST_METHOD']=="POST"){
  if(empty($Misplaced &_FILES['photo']['tmp_name'])  && $_FILES['photo']['error']  != 0){
    echo ‘没有文件被上传’;
}else{
   move_uploaded_file($_FILES['photo']['tmp_name'],'./upload/'.$_FILES['photo']['name']);
   }
}
```

 

![img](https://qq292383147.github.io/pictureLibrary/picture/php_mysql_ajax/4.png) 

 

```
Text/html:浏览器会进行解析<hr> ------> 解析为水平线

Text/plaiin:浏览器不会对这些内容进行解析： <hr>  ----> <hr>

Application/x-www-form-urlencoded:  POST方式传递普通键值对时需要设置的请求头 -->ajax

Multipart/form-data:告诉当前表单你的参数的编码格式有多种，并且，这些数据将来会以

formdata的形式包装
```

 

## 文件的上传步骤

1. 选择文件

2. 将文件数据作为参数传递给服务器

3. 接收用户数据

4. 服务器会自动的将文件存储到临时目录，如果你没有后续的操作，那么当程序结束的时候，文件会自动被删除

5. 将文件从临时目录移到你的文件存放目录（这一步是真正的将文件永久的存储在服务器端）

![img](https://qq292383147.github.io/pictureLibrary/picture/php_mysql_ajax/5.png) 

![img](https://qq292383147.github.io/pictureLibrary/picture/php_mysql_ajax/6.png) 

$_FILES数组

Type属性为file的input元素可以通过表单提交文件（上传文件），服务端PHP可以通过`$_FILES`获取上传的文件信息。

 

![img](https://qq292383147.github.io/pictureLibrary/picture/php_mysql_ajax/7.png) 

文件上传后，文件信息自动保存在预定义变量$_FILES数组中。

假设myFile为文件域的name属性值

```php
$_FILES[‘myFile’][’name’]   #文件的原始名称

$_FILES[‘myFile’][‘tmp_name’]   #文件的临时路径，默认为c:/windows/temp (运行窗口 -->temp)  没有直接将文件上传至Apache服务器的根目录

$_FILES[‘myFile’][‘type’]    #文件的内容类型：image/jpeg,image/png,image/gif,text/html，text/javascript

$_FILES[‘myFile’][‘error’]    #文件上传的错误代号。0代表没有发生错误

$_FILES[‘myFile’]’size’]      #文件大小（单位为byte，字节）
```



 

**关于文件上传的完整步骤**

1、设计表单

2、接收数据：判断<font color="#0fe">$_FILES’myFile’</font>是否为空

3、判断错误：<font color="#0fe">$_FILES’myFile’</font>.出错提示错误xx

4、此时文件在临时路径，如果需要将上传后的文件移动到某个指定位置，需要使用<font color="#0fe">move_uploaded_file()</font>函数移动到网站永久路径

move_upload_file(临时路径<font color="#0fe">$_FILES’myFile’</font>,永久路径);

 

代码：

```php
<?php

// 如果选择了文件 $_FILES['file']['error'] => 0
// 详细的错误码说明：http://php.net/manual/zh/features.file-upload.errors.php
if ($_FILES['file']['error'] === 0) {
  // PHP 在会自动接收客户端上传的文件到一个临时的目录
  $temp_file = $_FILES['file']['tmp_name'];
  // 我们只需要把文件保存到我们指定上传目录
  $target_file = '../static/uploads/' . $_FILES['file']['name'];
  if (move_uploaded_file($temp_file, $target_file)) {
    $image_file = '/static/uploads/' . $_FILES['file']['name'];
  }
}
```

 

## 使用文件上传和验证功能

```php
<?php 
function register(){
  //验证用户数据是否正确
  if(!isset($_POST['userName']) || trim($_POST['userName'])=== "" ){
    echo '请输入姓名';
    //1.如果在php结构中直接写return，那么当运行到return代码的时候，整个php文件的执行就结束了
    //2.如果在方法中写return，那么这个return就只能结束这个方法的执行
  return;

  }
  if(!isset($_POST['nickName']) || trim($_POST['nickName'])==="") {

    echo '请输入昵称';
  return;

  }
  //实现图片的上传操作
  print_r($_FILES);
  //判断图片上传操作是否成功
  if (empty($Misplaced &_FILES['photo']['tmp_name']) && $_FILES['photo']['error']!=0) {
    echo '图片上传失败';
  return;

  }
  //图片上传成功，我们需要去获取上传成功之后的图片名称
  $picName = $_FILES['photo']['name'];
  $ext = strrchr($picName,".");
  $finaName = time().rand(1000,9999).$ext;
  //将这个文件名称添加到$_POST中
  $_POST[] = $finaName;
  move_uploaded_file($_FILES['photo']['tmp_name'],$finaName);
  print_r($_POST);
  //数据的写入：明确数据写入的格式 qq|qq|123|123|男|1
  // implode：它可以将关联的数据以指定分隔符分隔，转换为字符串
  // explode：他可以将字符串以指定的分隔符分隔，生成关联数组
  $str = implode($_POST,"|");

  // 将数据写入到文件
  file_put_contents("data.txt",$str."\n",FILE_APPEND);
  }

  // 判断用户是提交的post请求
  if($_SERVER["REQUEST_METHOD"]==="POST"){
    register();
  }

?>
```

 

## 上传的限制，修改最大值--->改 php.ini

![img](https://qq292383147.github.io/pictureLibrary/picture/php_mysql_ajax/8.png) 

## 上传文件的最小值与最大值的范围是： 8M-20M

![img](https://qq292383147.github.io/pictureLibrary/picture/php_mysql_ajax/9.png) 

 

## JSON

是一种通过普通字符串描述数据的手段，用于表示有结构的数据。

 

## 数据类型

Null、string、number、boolean、object、array

注意：

> 1.JSON中属性名称必须用双引号包裹<br>
> 2.JSON中表述字符串必须使用双引号<br>
> 3.JSON中不能有单行或多行注释<br>
> 4.JSON没有undefined这个值<br>

 

## 列表数据

> JSON反序列化
> json_decode需要注意第二个参数
> 如果希望以关联数组的方式而非对象的方式操作数据，可以将json_decode的第二个参数设置为true

 

 

## 删除数据

一般情况下，如果需要超链接点击发起的请求可以传递参数，我们可以采用？的方式

```php
<a href="/delete.php?id=123">删除</a>
```

 

![img](https://qq292383147.github.io/pictureLibrary/picture/php_mysql_ajax/10.png) 

 

### 设置响应文件类型

```php
header('Content-Type: text/css');
```


### 设置响应头 <error：乱码，系统默认编码为utf-8>


```html
  header('Content-Type:text/html;charset=GB2312')
```

### 重定向（跳转到其他网页）

```php
header('Location: https://www.baidu.com');
```



### 下载文件

```php
// 让文件下载

header('Content-Type: application/octet-stream');

// 设置默认下载文件名

header('Content-Disposition: attachment; filename=demo.txt');
```

 

### GET

字面意思：拿，获取

### POST

字面意思：发，给

 

## cookie 和session 的区别详解

二者的定义：

当你在浏览网站的时候，WEB 服务器会先送一小小资料放在你的计算机上，Cookie 会帮你在网站上所打的文字或是一些选择，

都纪录下来。当下次你再光临同一个网站，WEB 服务器会先看看有没有它上次留下的 Cookie 资料，有的话，就会依据 Cookie

里的内容来判断使用者，送出特定的网页内容给你。 Cookie 的使用很普遍，许多有提供个人化服务的网站，都是利用 Cookie

来辨认使用者，以方便送出使用者量身定做的内容，像是 Web 接口的免费 email 网站，都要用到 Cookie。

 

具体来说cookie机制采用的是在客户端保持状态的方案，而session机制采用的是在服务器端保持状态的方案。

同时我们也看到，由于采用服务器端保持状态的方案在客户端也需要保存一个标识，所以session机制可能需要借助于cookie机制

来达到保存标识的目的，但实际上它还有其他选择。

cookie机制。正统的cookie分发是通过扩展HTTP协议来实现的，服务器通过在HTTP的响应头中加上一行特殊的指示以提示

浏览器按照指示生成相应的cookie。然而纯粹的客户端脚本如JavaScript或者VBScript也可以生成cookie。而cookie的使用

是由浏览器按照一定的原则在后台自动发送给服务器的。浏览器检查所有存储的cookie，如果某个cookie所声明的作用范围

大于等于将要请求的资源所在的位置，则把该cookie附在请求资源的HTTP请求头上发送给服务器。

cookie的内容主要包括：名字，值，过期时间，路径和域。路径与域一起构成cookie的作用范围。若不设置过期时间，则表示这个cookie的生命期为浏览器会话期间，关闭浏览器窗口，cookie就消失。这种生命期为浏览器会话期的cookie被称为会话cookie。

会话cookie一般不存储在硬盘上而是保存在内存里，当然这种行为并不是规范规定的。若设置了过期时间，浏览器就会把cookie

保存到硬盘上，关闭后再次打开浏览器，这些cookie仍然有效直到超过设定的过期时间。存储在硬盘上的cookie可以在不同的浏

览器进程间共享，比如两个IE窗口。而对于保存在内存里的cookie，不同的浏览器有不同的处理方式

session机制。session机制是一种服务器端的机制，服务器使用一种类似于散列表的结构（也可能就是使用散列表）来保存信息。

​          当程序需要为某个客户端的请求创建一个session时，服务器首先检查这个客户端的请求里是否已包含了一个session标识

（称为session id），如果已包含则说明以前已经为此客户端创建过session，服务器就按照session id把这个session检索出来

使用（检索不到，会新建一个），如果客户端请求不包含session id，则为此客户端创建一个session并且生成一个与此session相

关联的session id，session id的值应该是一个既不会重复，又不容易被找到规律以仿造的字符串，这个session id将被在本次响应

中返回给客户端保存。保存这个session id的方式可以采用cookie，这样在交互过程中浏览器可以自动的按照规则把这个标识发送给

服务器。一般这个cookie的名字都是类似于SEEESIONID。但cookie可以被人为的禁止，则必须有其他机制以便在cookie被禁止时

仍然能够把session id传递回服务器。

经常被使用的一种技术叫做URL重写，就是把session id直接附加在URL路径的后面。还有一种技术叫做表单隐藏字段。就是服务器

会自动修改表单，添加一个隐藏字段，以便在表单提交时能够把session id传递回服务器。比如： 

```
<form name="testform" action="/xxx"> 
<input type="hidden" name="jsessionid" value="ByOK3vjFD75aPnrF7C2HmdnV6QZcEbzWoWiBYEnLerjQ99zWpBng!-145788764"> 
<input type="text"> 
</form> 
```

实际上这种技术可以简单的用对`action`应用`URL`重写来代替。

cookie 和session 的区别：

1、cookie数据存放在客户的浏览器上，session数据放在服务器上。

2、cookie不是很安全，别人可以分析存放在本地的COOKIE并进行COOKIE欺骗
   考虑到安全应当使用session。

3、session会在一定时间内保存在服务器上。当访问增多，会比较占用你服务器的性能
   考虑到减轻服务器性能方面，应当使用COOKIE。

4、单个cookie保存的数据不能超过4K，很多浏览器都限制一个站点最多保存20个cookie。

5、所以个人建议：
   将登陆信息等重要信息存放为SESSION
   其他信息如果需要保留，可以放在COOKIE中


Cookie需要解决三个问题：分发、内容和使用。


cookie的分发是通过扩展HTTP协议来实现的，服务器端通过在HTTP的响应由中加上一行特殊的指示以提示浏览器按照指示生成相应的cookie。


cookie的内容主要包括name(名字)、value(值)、maxAge(失效时间)、path(路径),domain(域)和secure


**name**：cookie的名字，一旦创建，名称不可更改。


**value**：cookie的值，如果值为Unicode字符，需要为字符编码。如果为二进制数据，则需要使用BASE64编码.


**maxAge**：cookie失效时间，单位秒。如果为正数，则该cookie在maxAge后失效。如果为负数，该cookie为临时cookie，关闭浏览器即失效，浏览器也不会以任何形式保存该cookie。如果为0，表示删除该cookie。默认为-1

 

**path**：该cookie的使用路径。如果设置为"/sessionWeb/"，则只有ContextPath为“/sessionWeb/”的程序可以访问该cookie。如果设置为“/”，则本域名下ContextPath都可以访问该cookie。

 

**domain**:域.可以访问该Cookie的域名。第一个字符必须为".",如果设置为".google.com",则所有以"google.com结尾的域名都可以访问该cookie",如果不设置,则为所有域名

 

**secure**：该cookie是否仅被使用安全协议传输。

 

cookie的使用是由浏览器按照一定的原则在后台自动发送给服务器。浏览器检查所有存储的cookie，如果某个cookie所声明的作用范围大于等于将要请求的资源所在的位置，则把该cookie附在请求资源的HTTP请求头上发送给服务器.

 

Session机制

 

Session机制是一种服务端的机制，服务器使用一种类似散列表的结构来保存信息。当程序需要为某个客户端的请求创建一个session的时候，服务器首先检查这个客户端里的请求里是否已包含了一个session标识--sessionID，如果已经包含一个sessionID，则说明以前已经为此客户端创建过session，服务器就按照sessionID把这个session检索出来使用（检索不到，可能会新建一个），如果客户端请求不包含sessionID，则为此客户端创建一个session并且声称一个与此session相关联的sessionID，sessionID的值应该是一个既不会重复，又不容易被找到规律以仿造的字符串(服务器会自动创建),这个sessionID将被在本次响应中返回给客户端保存。

 

保存sessionID的方式

 

1，使用Cookie.此时Cookie不再用作认证,只是作为载体,存储sessionID

 

2，URL重写：因为cookie可以被人为禁止，所以为了保证sessionID能够被传递给服务器，使用URL重写也是一种解决方法。如,

 

href="<%=response.encodeURL("index.jsp") %>"

 

写好后URL是这样的

 

href="index.jsp;jsessionid=0CCD096E7F8D97B0BE608AFDC3E1931E"

 

3, 隐藏表单提交.将sessionId放在隐藏表单中

 

实际上这几种方式最方便的还是cookie,其他两种方式都各有弊端,URL重写的弊端是要对所有的URL都重写,非常繁琐.表单隐藏字段的弊端是只能局限于表单提交,如果是单纯的文本链接则不能提供会话跟踪

 

Cookie和Session之间的区别

 

1.Cookie数据存放在客户的浏览器(本地),session数据放在服务器上

 

2.Cookie不如session安全，别人可以分析存放在本地的Cookie并进行Cookie欺骗,所以出于安全性的考虑应当使用Session

 

3.Session会在一定时间内保存在服务器上。当访问增多,会占用较多的服务器资源,所以出于性能考虑则应当使用cookie

 

单个cookie保存的数据不能超过4k,很多浏览器都限制一个站点最多保存20个cookie.实际上为了性能考虑,不论是cookie还是session,其中的信息都应当短小精悍

 

session因为是保存在服务器上,所以不支持跨域的访问

 

摘要

Cookie：

Setcookie(name,value,expire,path,domain)

Expire:一定要参数当前时间：time() + 10

--->有效期10秒

Path:path是以当前网站根目录做为参照/目录名称

通过$_cookie获取存储的数据

if(isset($_cookie[‘isLogin’]) )

删除

Setcookie(name,过期时间)

Setcookie(name,false)

Setcookie(name,””)

Setcookie(name)

 

Session:

1. session_start();

A. 随机生成session_id

B. 根据session_id创建数据存储文件

C. 将session_id以cookie的形式返回

2. 赋值和取值都是通过$_session

3. 删除session

Unset($_SESSION[key])

$_session= []

Session_destroy()

-->会同时销毁文件

## SQL

-- 注释使用--

-- 实现数据操作

-- 增加删除和修改返回受影响的行数--修改表数据

-- 查询是返回结果集--虚拟表

 

-- 增加

-- 语法：insert [into] 表名[(字段名列表)] values(值列表)

-- 细节：

-- 1.值的数量，类型和顺序需要和字段列表的完全一致

-- 2.如果在表名后面没有指定字段,意味着需要对表的所有字段添加值

-- 3.标识列不要人为设置，一般给null

-- 4.如果字段有默认值，也可能传入default

-- 5.如果是非空字段，建议一定要赋值

-- 6. 有标记列的字段一般赋值null

INSERT into songs VALUES('qq','qq','qq','2018-8-8')

INSERT into songs(singer,title,album,pubtime) VALUES('qq','qq','qq','2018-8-8')

INSERT into songs(title,album,pubtime) VALUES('qaaq','qaq','2018-8-8')

INSERT into songs(singer,album,pubtime) VALUES(DEFAULT,'qaaq','2018-8-8')

INSERT into songs VALUES(null,'qq','qq','qq','2018-8-8',DEFAULT)

 

-- 常见错误

-- Column count doesn't match value count at row 1:值的数量和字段数量不匹配

-- Unknown column 'ablum' in 'field list'  列不存在，一般是列名写错了

 

-- 删除:删除是针对数据行而言，删除一定要考虑是否有条件

-- 语法 

-- DELETE FROM 表：删除整个表的数据行

-- DELETE FROM 表 WHERE 条件 

-- 多条件的连接使用 !-not &&-and  ||-or

DELETE from songs

DELETE from songs where id = 7

DELETE from songs where title='aa' and album='aa'

​	

 

-- 修改:一定要考虑是否有条件

-- 语法：

-- UPDATE 表名 set 字段=新值,字段2=新值2 WHERE 条件

-- 值可以是具体的数据，也可以是简单的表达式

UPDATE songs set singer = CONCAT(singer,'123')

UPDATE songs set title='李四的歌',album='我是李四' where id= 10

 

 

-- 查询 

-- 语法：select 字段列表|* from 表 WHERE 查询条件

```mysql
SELECT \* from songs

select \* from songs where album='qq'

SELECT \* from songs where isdelete = 0
```

 

![img](https://qq292383147.github.io/pictureLibrary/picture/php_mysql_ajax/11.png) 

![img](https://qq292383147.github.io/pictureLibrary/picture/php_mysql_ajax/12.png) 

![img](https://qq292383147.github.io/pictureLibrary/picture/php_mysql_ajax/13.png) 

![img](https://qq292383147.github.io/pictureLibrary/picture/php_mysql_ajax/14.png) 

![img](https://qq292383147.github.io/pictureLibrary/picture/php_mysql_ajax/15.png) 

![img](https://qq292383147.github.io/pictureLibrary/picture/php_mysql_ajax/16.png) 

![img](https://qq292383147.github.io/pictureLibrary/picture/php_mysql_ajax/17.png) 

![img](https://qq292383147.github.io/pictureLibrary/picture/php_mysql_ajax/18.png) 

![img](https://qq292383147.github.io/pictureLibrary/picture/php_mysql_ajax/19.png) 

 

Date类型的处理

![img](https://qq292383147.github.io/pictureLibrary/picture/php_mysql_ajax/20.png) 

 

![img](https://qq292383147.github.io/pictureLibrary/picture/php_mysql_ajax/21.png) 

 

![img](https://qq292383147.github.io/pictureLibrary/picture/php_mysql_ajax/22.png) 

## 请求

HTML请求3个组成部分与XMLHttpRequest方法的对应关系

### 1、请求行：

```php
xhr.open('get','index.php');
```

### 2、请求头：

```php
xhr.setRequestHeader('Context-Type' , 'text/html');
```



### 3、请求主体：(get请求可以不设置)

```php
xhr.send(null);
```

 

### 响应：(onreadystatechange是javascript的事件的一种，其意义在于监听XMLHttpRequest的状态)

#### 1、获取状态行(包括状态码&状态信息)

xhr.status  	  //状态码

xhr.statusText   //状态信息

### 3、 获取响应头

xhr.getRespnseHeader(‘Context-Type’);  //获取指定头信息

xhr.getAllResponseHeaders();			//获取所有响应头信息

xhr.open()  //发起请求，可以是get\post方式

xhr.setRequestHeader()  //设置请求头

xhr.send()   //发送请求主体get方式使用xhr.send(null);

xhr.onreadystatechange = function(){}  //监听响应状态

 

readstate 属性有五个状态：

xhr.readyState = 0 时，(未初始化)还没有调用send()方法

xhr.readyState = 1 时，(载入)已调用send()方法，正在发送请求

xhr.readyState = 2 时，(载入完成)send()方法执行完成，已经接收到全部响应内容

xhr.readyState = 3时， (交互)正在解析响应内容

xhr.readyState = 4时，(完成)响应内容解析完成，可以在客户端调用了

 

xhr.getAllResponseHeaders() 获取全部响应头信息

xhr.getResponseHeader('key') 获取指定头信息

xhr.responseText、xhr.responseXML都表示响应主体

## JSON

即JavaScript Object Notation 另一种轻量级的文本数据交换格式，独立于语言

 

### 1.ajax概念：

​    为什么需要ajax:提升用户体现，可以实现页面局部刷新

 

### 2.ajax：异步的js and xml

 

### 3.异步和同步

​    异步：同时可以做多个事情。异步非阻塞   异步的执行顺序不依赖于书写顺序  异步往往会伴随着回调

​    同步：事情需要一步一步来执行，在执行一个操作的时候，另外的操作就需要等待

 

### 4.使用异步对象实现请求和响应的接收

​    1.使用XMLHttpRequest:

​        var xhr = new XMLHttpRequest()

​    2.使用异步对象发送请求

​        设置请求行

​            如果有参数，get方式需要在url中拼接参数

​            xhr.open(请求方式，请求url)

​        设置请求头：

​            get不需要设置，post需要以下设置：

​            xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded')

​        设置请求体：

​            get方式没有请求体，post才会在这个位置设置请求体

​            xhr.send(请求体)

 

​    3.接收响应

​        添加对响应状态和异步对象执行状态的监听

​        xhr.onreadystatechange = function(){}

​        一个成功的响应有两个前提：服务器成功响应  数据解析完毕可以在客户端使用

​        if(xhr.status == 200 && xhr.readyState == 4){

​            // 接收响应

​            xhr.responseText;

​        }

 

​    4.json格式数据的转换

​        JSON.parse(jsonStr):将json格式字符串转换为js变量(数组，对象)

​        JSON.stringify(js变量):将js变量转换为json格式字符串

 

 

### 5.get和post请求方式在异步处理时的异同

​    	发送请求时的三句代码都不一样

​    	请求行：

​        	get:如果有参数，应该在url中拼接参数

​        	post:不在url拼接参数

​    	请求头：

​        	get:不需要设置请求头

​        	post:需要设置 								xhr.setRequestHeader('Content-Type','application/x-www/form-urlencoded')

​    	请求体：

​        	get:没有请求体

​        	post:如果有参数在请求体中传递参数

 

​    	接收响应：

​        	get和post代码完全一致

​        	但是接收数据之后的解析过程不一样

 

## POST和GET有什么区别？

1、 GET主要用于从服务器查询数据，POST用于向服务器提交数据

2、 GET通过URL传递数据，POST通过http请求体传递数据

3、 GET传输数据量有限制，不能大于2kb，POST传递的数据量较大，一般大量的数据提交都是通过POST方式

4、 GET安全性较低，容易在URL中暴漏数据，POST安全性较高

 

 

**使用模板实现数据遍历**

![img](https://qq292383147.github.io/pictureLibrary/picture/php_mysql_ajax/23.png) 

 

在script标签中设置type为：text/template,让浏览器不认识的格式

![img](https://qq292383147.github.io/pictureLibrary/picture/php_mysql_ajax/24.png) 

**添加模板数据**

![img](https://qq292383147.github.io/pictureLibrary/picture/php_mysql_ajax/25.png) 

**在结构中设置方式  <%%>表示script中的逻辑表达方式，看以下图**

![img](https://qq292383147.github.io/pictureLibrary/picture/php_mysql_ajax/26.png) 

![img](https://qq292383147.github.io/pictureLibrary/picture/php_mysql_ajax/27.png) 

**获取并生成数据（遍历）**

![img](https://qq292383147.github.io/pictureLibrary/picture/php_mysql_ajax/28.png) 

**理解传入的数据是数组还是对象，对象可以直接用，数组需要转换**

 

 

Test与exec函数的作用和区别

![img](https://qq292383147.github.io/pictureLibrary/picture/php_mysql_ajax/29.png) 

 

## 一：JQ中的ajax

```js
    $.ajax({

        type:请求方式

        url:请求url

        data:参数

        timeout:设置超时

        dataType:返回值的类型

        beforeSend:请求发送之前的回调

        success:响应成功后的回调

        error:请求失败时的回调

        complete:无论请求是否成功都会执行的回调

    })

    $.get(url,data,success,dataType)

    $.post(url,data,success,dataType)
```

 

 

## 二：模板引擎的使用

​    1.作用：可以代替拼接字符串的操作

​    2.步骤

​        1.请求接收响应数据

​        2.创建模板

```js
script标签创建模板 <script type='text/template' id=''></script>
```

​        3.创建模板内容结构

​            原生写法

​                逻辑表达式：<% 逻辑表达式 %>

​                输出表达式：<%= 内容表达式 %>

​            简写写法：

​                逻辑表达式：{{ 逻辑表达式 }}

​                输出表达式：{{ 内容表达式 }}

​    3.使用模板的原则

​        1.如果传入的数据是对象，就直接传入对象

​        2.如果传入的数据是数组，就包装为对象

 

## 同源

同源策略是浏览器的一种安全策略，所谓同源是指，域名，协议，端口完全相同。

## 跨域

不同源则跨域

1. 不允许进行DOM操作

2. 不能进行ajax请求

```js
// 服务器跨域：cross-origin-resource-sharing

header( 'Access-Control-Allow-Origin:*' ); 

header( 'Access-Control-Allow-Origin:http://www.study.com');
```

 

## 1.JSONP的由来

根据浏览器同源策略，所谓同源就是协议、主机、端口号都相同时成为同源。a 域的js不能直接访问 b域名的信息，但是script 标签的src属性可以跨域引用文件，jsonp是请求之后后台包装好一段json，并且把数据放在一个callback函数，返回一个js文件，动态引入这个文件，下载完成js之后，会去调用这个callback,通过这样访问数据。

## 2. JSONP有什么用

由于同源从略的限制，XMLHttpRequest只允许请求前源（域名、协议、端口）的资源，为了实现跨域请求，可以通过script标签实现跨域请求，然后再服务端输出JSON数据并执行回调函数，从而解决跨域数据请求

## 3. 如何使用JSONP

HTML代码

![img](https://qq292383147.github.io/pictureLibrary/picture/php_mysql_ajax/30.png)

PHP代码

![img](https://qq292383147.github.io/pictureLibrary/picture/php_mysql_ajax/31.png)

## 4. JSONP原理

首先在客户端注册一个callback，然后把callback的名字传给服务器。此时，服务器先生成json数据，然后以javascript语法的方式，生成function，function名字就是传递上来I带参数jsonp。最后将json数据直接以入参的方式，放置function中，这样就生成js语法的文档，返回给客户端。客户端浏览器，解析script变迁，并执行返回javascript文档，此时数据作为参数，传入了客户端预先定义好的callback函数里。简单的说，就是利用script标签没有跨域限制的“漏洞”来达到与第三方通讯的目的。

![img](https://qq292383147.github.io/pictureLibrary/picture/php_mysql_ajax/32.png)

## json 是一种数据格式，jsonp 是一种数据调用的方式，带callback的json就是jsonp

前端向后台发送请求有几种方式？

1、 link标签的href属性

2、 script标签的src属性

3、 img标签的src属性

4、 ajax发送请求

5、 表单提交发送请求

6、 a标签的href发送请求

7、 iframe的src属性发送请求

![img](https://qq292383147.github.io/pictureLibrary/picture/php_mysql_ajax/33.png) 

