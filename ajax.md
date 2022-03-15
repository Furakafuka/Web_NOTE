# Ajax

## day1

### 基本概念

1. URL:统一资源定位符

   1. 组成
      1. ![image-20220302171100824](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220302171100824.png)
      2. 客户端与服务器之间的通信协议
      3. 存有该资源的服务器名称
      4. 资源在服务器上具体的存放位置

2. 客户端与服务器的通信过程

   1. ![image-20220302171206326](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220302171206326.png)

   2. 通信过程分析

      1. 在开发者工具的NetWork-Doc查看

         ![image-20220302171415188](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220302171415188.png)

   3. 网页请求数据
      1. 如果要在网页中请求服务器上的数据资源，则需要用到==XMLHttpRequest==对象
      2. get请求资源
      3. post发送资源

3. Ajax

   1. 在网页中利用 XMLHttpRequest 对象和服务器进行数据交互的方式，就是Ajax。

​	

### JQuery中的Ajax

1. $.get()
   1. ```$.get(url, [data], [callback])```
   2. url:要请求的资源地址
   3. data:请求资源期间要携带的参数
   4. callback:请求成功时的回调函数
   5. $.get()发起==不带参数==的请求:
      1. 所有的Ajax请求都可通过XHR查看
      2. 直接提供请求的 URL 地址和请求成功之后的回调函数即可
   6. $.get()发起带参数的请求
      1. 第二个参数为一个参数对象,请求指定信息

2. $.post()向服务器提交数据

   1. ```$.post(url, [data], [callback])```

   2. ```javascript
      $.post(
      'http://www.liulongbin.top:3006/api/addbook', // 请求的URL地址
      { bookname: '水浒传', author: '施耐庵', publisher: '上海图书出版社' }, // 提交的数据
      function(res) { // 回调函数
      console.log(res)
      }
      )
      ```

      

3. #.ajax()函数

   1. 可以发送get和post

   2. ```JavaScript
      $.ajax({
      type: '', // 请求的方式，例如 GET 或 POST
      url: '', // 请求的 URL 地址
      data: { },// 这次请求要携带的数据
      success: function(res) { } // 请求成功之后的回调函数
      })
      ```

4. 接口

   1. 使用 Ajax 请求数据时，被请求的 URL 地址，就叫做数据接口

   2. 接口测试工具:PostMan

   3. get请求使用方法:![image-20220303163934223](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220303163934223.png)

   4. post请求使用方法:

      ![image-20220303164126414](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220303164126414.png)

      (要选择==body==面板)

5. 接口文档

   1. 接口文档，顾名思义就是接口的说明文档，它是我们调用接口的依据。

   2. 组成:

      1. 接口名称：用来标识各个接口的简单说明，如登录接口，获取图书列表接口等。

      2. 接口URL：接口的调用地址。

      3. 调用方式：接口的调用方式，如 GET 或 POST。

      4. 参数格式：接口需要传递的参数，每个参数必须包含参数名称、参数类型、是否必选、参数说明这4项内容。

      5. 响应格式：接口的返回值的详细描述，一般包含数据名称、数据类型、说明3项内容。

      6. 返回示例（可选）：通过对象的形式，例举服务器返回数据的结构

      7. 示例:![image-20220303164455867](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220303164455867.png)

         ![image-20220303164508204](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220303164508204.png)

         ![image-20220303164529142](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220303164529142.png)

         

## day2

### form表单

1. 表单在网页中主要负责数据采集功能。

2. 组成部分

   1. ```JavaScript
      <form>
      <input type="text" name="email_or_mobile" />
      <input type="password" name="password" />
      <input type="checkbox" name="remember_me" checked />
      <button type="submit">提交</button>
      </form>
      ```

   2. 组成部分:表单标签 表单域 表单按钮

3. \<form>标签的属性

   1. action:向何处提交表单数据(默认值为当前页面的URL地址)
      1. 当提交表单后，页面会立即跳转到 action 属性指定的 URL 地址
   2. target:在何处打开 action URL
      1. _blank:在新窗口打开
      2. _Self:在当前页面打开
   3. method:以何种方式提交
      1. get:表示==通过URL地址的形式==，把表单数据提交到 action URL
      2. post:以form data的形式提交.适合大量数据提交
   4. enctype:编码方式
      1. 默认值:application/x-www-form-urlencoded(在发送前编码所有字符)
      2. multipart/form-data:不对字符编码。
      3. 设计文件上传时,一定要改成==multipart/form-data==

4. 同步提交

   1. 通过点击 submit 按钮，触发表单提交的操作，从而使页面跳转到 action URL 的行为，叫做表单的同步提交。
   2. 缺点
      1. 整个页面的数据都会丢失
      2. 整个页面会发生跳转，跳转到 action URL 所指向的地址，用户体验很差。
   3. 解决:表单提交数据,Ajax提交数据

5. 通过Ajax提交表单数据

   1. 监听表单提交事件

      ```JavaScript
      $('#form1').submit(function(e) {
      alert('监听到了表单的提交事件')
      })
      $('#form1').on('submit', function(e) {
      alert('监听到了表单的提交事件')
      })
      ```

   2. 阻止表单默认提交行为

      ```javascript
      $('#form1').submit(function(e) {
      // 阻止表单的提交和页面的跳转
      e.preventDefault()
      })
      $('#form1').on('submit', function(e) {
      // 阻止表单的提交和页面的跳转
      e.preventDefault()
      })
      ```

   3. 快速获取表单的数据
      1. ```$(selector).serialize()```
      2. 返回形式:username=用户名的值&password=密码的值(使用&分割)
      3. ==必须为表单添加name属性==
      4. 快速清空表单内容:```$('#formAddCmt')[0].reset()```



### 模板引擎

1. 以前是通过字符串拼接来渲染UI结构,使用模板引擎解决,减少了字符串的拼接操作

2. art-template模板引擎

   1. template("模板的id",需要渲染的数据)

   2. 定义模板:模板的html结构需要定义到Script中(不要当作js解析,要当作HTML解析)

      ```javascript
      <script type="text/html" id="tpl"><script>
      ```

   3. 标准语法:{{}}:变量输出,循环数组

   4. 渲染:$().html(template函数的返回值)

3. 常用语法

   1. 原文输出:输出的值中包括HTML标签结构,需要使用原文输出

      1. ```{{@ value}}```

   2. 条件输出

      1. ```{{if value}} 按需输出的内容 {{/if}}```

   3. 循环输出

      1. ```JavaScript
         {{each arr}}
         {{$index}} {{$value}}
         {{/each}}
         ```

   4. 过滤器

      1. ```{{value | filterName}}```
      2. 过滤器语法:```template.defaults.imports.filterName = function(value){/*return处理的结果*/}```
      3. 示例:![image-20220303193213365](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220303193213365.png)

   4. 正则表达式

      1. 语法:```exec()```

      2. 示例:

         ```javascript
         var str = '<div>我是{{name}}</div>'
         var pattern = /{{([a-zA-Z]+)}}/
         var patternResult = pattern.exec(str)
         console.log(patternResult)
         // 得到 name 相关的分组信息
         // ["{{name}}", "name", index: 7, input: "<div>我是{{name}}</div>", groups: undefined]
         ```

      3. 多次匹配:```/{{\s*([a-zA-Z]+)\s*}}/```

      4. while循环

         1. ```javascript
            while(patternResult = pattern.exec(str)) {
            str = str.replace(patternResult[0], patternResult[1])
            }
            ```





## day3

### XHR(XMLHttpRequest)

1. 概念:

   1. 浏览器提供的 Javascript 对象，通过它，可以请求服务器上的数据资源。之
      前所学的 jQuery 中的 Ajax 函数，就是基于 xhr 对象封装出来的。

      ![image-20220303195845961](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220303195845961.png)

2. 使用xhr发起GET请求

   ```js
   // 1. 创建 XHR 对象
   var xhr = new XMLHttpRequest()
   
   // 2. 调用 open 函数，指定 请求方式 与 URL地址
   xhr.open('GET', 'http://www.liulongbin.top:3006/api/getbooks')
   
   // 3. 调用 send 函数，发起 Ajax 请求
   xhr.send()
   
   // 4. 监听 onreadystatechange 事件
   xhr.onreadystatechange = function() {
       
       
   // 4.1 监听 xhr 对象的请求状态 readyState ；与服务器响应的状态 status
   if (xhr.readyState === 4 && xhr.status === 200) {
   // 4.2 打印服务器响应回来的数据
   console.log(xhr.responseText)
       
       
   	}	
   }
   ```

    1. readystate属性:

       ![image-20220303200511458](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220303200511458.png)

3. 查询字符串

   1. 查询字符串（URL 参数）是指在 URL 的末尾加上用于向服务器发送信息的字符串（变量)
   2. 格式:在?后面加上参数=值.使用&符号分割

4. get请求携带参数的本质

   1. 当需要携带参数的时候，本质上，都是直接将参数以查询字符串的形式，追加到 URL 地址的后面，发送到服务器的

5. URL编码

   1. URL需要中文时,必须对中文字符进行编码
   2. * encodeURI() 编码的函数
      * decodeURI() 解码的函数

6. 使用xhr发起POST请求

   1. ```JavaScript
      // 1. 创建 xhr 对象
      var xhr = new XMLHttpRequest()
      
      // 2. 调用 open()
      xhr.open('POST', 'http://www.liulongbin.top:3006/api/addbook')
      
      // 3. 设置 Content-Type 属性（固定写法）
      xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
      
      // 4. 调用 send()，同时将数据以查询字符串的形式，提交给服务器
      xhr.send('bookname=水浒传&author=施耐庵&publisher=天津图书出版社')
      
      // 5. 监听 onreadystatechange 事件
      xhr.onreadystatechange = function() {
      if (xhr.readyState === 4 && xhr.status === 200) {
      console.log(xhr.responseText)
      	}
      }
      ```

      1. Content-Type是固定的写法





### 数据交换格式

1. 两种交换格式:XML和JSON

2.  XML

   1. ```xml
      <note>
      <to>ls</to>
      <from>zs</from>
      <heading>通知</heading>
      <body>晚上开会</body>
      </note>
      ```

   2. 缺点:
      1. XML 格式臃肿，和数据无关的代码多，体积大，传输效率低
      2. 在 Javascript 中解析 XML 比较麻烦

3. JSON

   1. JSON 就是 Javascript 对象和数组的字符串表示法
   2. JSON 的本质是字符串

4. JSON结构

   1. 对象结构

      1. 数据结构为 { key: value, key: value, … } 的键值对结构

      2. ```json
         {
         "name": "zs",
         "age": 20,
         "gender": "男",
         "address": null,
         "hobby": ["吃饭", "睡觉", "打豆豆"]
         }
         ```

   2. 数组结构:```[ { "name": "zs", "age": 20}, { "name": "ls", "age": 30} ]```

5. JSON注意事项

   1. 属性名必须使用双引号包裹
   2. 字符串类型的值必须使用双引号包裹
   3. JSON 中不允许使用单引号表示字符串
   4. JSON 中不能写注释
   5. JSON 的最外层必须是对象或数组格式
   6. 不能使用 undefined 或函数作为 JSON 的值

6. JSON和JS对象的互转

   1. JSON->JS对象:```JSON.parse()```
   2. JS对象->JSON: ```JSON.stringify()```



### 封装Ajax函数

### XHR高级用法

1. 设置HTTP请求时限```xhr.timeout = 3000```

   1. 超时回调函数:

   ```javascript
   xhr.ontimeout = function(event){
   alert('请求超时！')
   }
   ```

2. FormData对象管理表单数据

   1. 基本操作:

      ```javascript
      // 1. 新建 FormData 对象
      var fd = new FormData()
      // 2. 为 FormData 添加表单项
      fd.append('uname', 'zs')
      fd.append('upwd', '123456')
      // 3. 创建 XHR 对象
      var xhr = new XMLHttpRequest()
      // 4. 指定请求类型与URL地址
      xhr.open('POST', 'http://www.liulongbin.top:3006/api/formdata')
      // 5. 直接提交 FormData 对象，这与提交网页表单的效果，完全一样
      xhr.send(fd)
      ```

   2. 获取网页表单

      ```JavaScript
      // 获取表单元素
      var form = document.querySelector('#form1')
      // 监听表单元素的 submit 事件
      form.addEventListener('submit', function(e) {
      e.preventDefault()
      // 根据 form 表单创建 FormData 对象，会自动将表单数据填充到 FormData 对象中
      var fd = new FormData(form)
      var xhr = new XMLHttpRequest()
      xhr.open('POST', 'http://www.liulongbin.top:3006/api/formdata')
      xhr.send(fd)
      xhr.onreadystatechange = function() {}
      }
      ```

3. 上传文件

   1. 定义UI结构

      ```html
      <!-- 1. 文件选择框 -->
      <input type="file" id="file1" />
      <!-- 2. 上传按钮 -->
      <button id="btnUpload">上传文件</button>
      <br />
      <!-- 3. 显示上传到服务器上的图片 -->
      <img src="" alt="" id="img" width="800" />
      ```

   2. 验证是否选择文件

      ```javascript
      // 1. 获取上传文件的按钮
      var btnUpload =document.querySelector('#btnUpload')
      
      // 2. 为按钮添加 click 事件监听
      btnUpload.addEventListener('click', function() {
          
      // 3. 获取到选择的文件列表
      var files =document.querySelector('#file1').files
      if (files.length <= 0) {
      return alert('请选择要上传的文件！')
      }
      // ...后续业务逻辑
      }
      ```

   3. 向FormData追加文件

      ```JavaScript
      // 1. 创建 FormData 对象
      var fd = new FormData()
      // 2. 向 FormData 中追加文件
      fd.append('avatar', files[0])
      ```

   4. 使用xhr发起请求

      ```js
      // 1. 创建 xhr 对象
      var xhr = new XMLHttpRequest()
      
      // 2. 调用 open 函数，指定请求类型与URL地址。其中，请求类型必须为 POST
      xhr.open('POST', 'http://www.liulongbin.top:3006/api/upload/avatar')
      
      // 3. 发起请求
      xhr.send(fd)
      ```

   5. 监听事件

      ```JavaScript
      xhr.onreadystatechange = function() {
      if (xhr.readyState === 4 && xhr.status === 200) {
          
      var data = JSON.parse(xhr.responseText)
      
      if (data.status === 200) { // 上传文件成功
      // 将服务器返回的图片地址，设置为 <img> 标签的 src 属性
      
      document.querySelector('#img').src = 'http://www.liulongbin.top:3006' + data.url
      } else { // 上传文件失败
      console.log(data.message)
      		}
      	}
      }
      ```

   6. 显示文件上传进度

      ```js
      // 创建 XHR 对象
      var xhr = new XMLHttpRequest()
      // 监听 xhr.upload 的 onprogress 事件
      
      xhr.upload.onprogress = function(e) {
      // e.lengthComputable 是一个布尔值，表示当前上传的资源是否具有可计算的长度
          
      if (e.lengthComputable) {
      // e.loaded 已传输的字节
      // e.total
      需传输的总字节
      var percentComplete = Math.ceil((e.loaded / e.total) * 100)
      }
      }
      ```

4. JQuery实现

   1. 定义UI结构

      ```JavaScript
      <!-- 导入 jQuery -->
      <script src="./lib/jquery.js"></script>
      <!-- 文件选择框 -->
      <input type="file" id="file1" />
      <!-- 上传文件按钮 -->
      <button id="btnUpload">上传</button>
      ```

   2. 是否选择文件

      ```JavaScript
      $('#btnUpload').on('click', function() {
      // 1. 将 jQuery 对象转化为 DOM 对象，并获取选中的文件列表
      var files = $('#file1')[0].files
      // 2. 判断是否选择了文件
      if (files.length <= 0) {
      return alert('请选择图片后再上传！‘)
      }
      })
      ```

   3. 向FormData追加文件

      ```js
      // 向 FormData 中追加文件
      var fd = new FormData()
      fd.append('avatar', files[0])
      ```

   4. 使用jQuery发起请求

      ```js
      $.ajax({
      method: 'POST',
      url: 'http://www.liulongbin.top:3006/api/upload/avatar',
      data: fd,
      // 不修改 Content-Type 属性，使用 FormData 默认的 Content-Type 值
      contentType: false,
      // 不对 FormData 中的数据进行 url 编码，而是将 FormData 数据原样发送到服务器
      processData: false,
      success: function(res) {
      console.log(res)
      }
      })
      ```

   4. 实现loading效果

      ```JavaScript
      // 自 jQuery 版本 1.8 起，该方法只能被附加到文档
      $(document).ajaxStart(function() {
      $('#loading').show()
      })
      ```

   5. ajax上传结束后会执行ajaxStop函数

      ```javascript
      // 自 jQuery 版本 1.8 起，该方法只能被附加到文档
      $(document).ajaxStop(function() {
      $('#loading').hide()
      })
      ```

### axios

1. 示例

   ```JavaScript
       <button id="btn1">发起get</button>
       <script>
           document.querySelector('#btn1').addEventListener('click',function(){
               var url='http://www.liulongbin.top:3006/api/get'
               var paramobj={name:'zs',age:20}
               
               
               axios.get(url,{params:paramobj}).then(function(res){
                   
                   
                   console.log(res.data)
               })
           })
       </script>
   ```

2. 发起POST请求

   1. 格式:

      ```JavaScript
      axios.post('url', { /*参数*/ }).then(callback)
      ```

3. 直接发起axois请求

   ```js
   axios({
   method: '请求类型',
   url: '请求的URL地址',
   data: { /* POST数据 */ },
   params: { /* GET参数 */ }
   }) .then(callback)
   ```





## day4

### 同源策略和跨域

1. 同源:如果两个页面的协议，域名和端口都相同，则两个页面具有相同的源

   1. 端口号默认:80

2. 同源策略:同源策略限制了从同一个源加载的文档或脚本如何与来自另一个源的资源进行交互。这是一个用于隔离潜在恶意文件的重要安全机制

   1. 例如:
      1. 无法读取非同源网页的 Cookie、LocalStorage 和IndexedDB
      2. 无法接触非同源网页的 DOM
      3. 无法向非同源地址发送 Ajax 请求

3. 跨域:同源指的是两个 URL 的协议、域名、端口一致，反之，则是跨域

4. 浏览器的拦截:

   ![image-20220303221745675](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220303221745675.png)

​	

### JSONP

1. 只支持GET请求,不支持POST

2. 可用于解决主流浏览器的跨域数据访问的问题。

3. ==\<script> 标签不受浏览器同源策略的影响==，可以通过 src 属性，请求非同源的 js 脚本

4. 在scrpit标签后添加callback=funciton来调用指定的函数

5. ==不属于Ajax请求==

6. 由于 JSONP 是通过 <script> 标签的 src 属性，来实现跨域数据获取的，所以，JSONP 只支持 GET 数据请求，不支持 POST 请求。

7. jQuery发起JSONP

   1. ```JavaScript
      $.ajax({
      url: 'http://ajax.frontend.itheima.net:3006/api/jsonp?name=zs&age=20',
      // 如果要使用 $.ajax() 发起 JSONP 请求，必须指定 datatype 为 jsonp
      dataType: 'jsonp',
      success: function(res) {
      console.log(res)
      }
      })
      ```

   2. 默认情况下，使用 jQuery 发起 JSONP 请求，会自动携带一个callback=jQueryxxx 的参数，jQueryxxx 是随机生成的一个回调函数名称

   3. 自定义参数和回调函数名称

      1. ```JavaScript
         // 发送到服务端的参数名称，默认值为 callback
          jsonp: 'callback',
         // 自定义的回调函数名称，默认值为 jQueryxxx 格式
         jsonpCallback: 'abc',
         ```
   
   4. jQuery 采用的是动态创建和移除 <script> 标签的方式，来发起 JSONP 数据请求。





### 防抖

1. 当事件被触发后，延迟 n 秒后再执行回调.如果在这 n 秒内事件又被触发，则重新计时
2. 事件触发n次时,只执行最后一次





### 节流

1. 可以减少一段时间内事件的触发频率

## day5

### HTTP协议简介

1. 三要素:主体,内容,方式

2. 通信协议:通信的双方完成通信所必须遵守的规则和约定

3. 网页内容又叫做超文本，因此网页内容的传输协议又叫做超文本传输协议（HyperText Transfer Protocol）,简称 HTTP 协议。

4. HTTP采用了请求/相应模型

   ![image-20220303222304882](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220303222304882.png)



### HTTP请求信息

1. 客户端发起的请求叫做 HTTP 请求，客户端发送到服务器的消息，叫做 HTTP 请求消息

2. 组成部分:请求行（request line）、请求头部（ header ） 、空行 和 请求体 4 个部分组成

   ![image-20220303222432297](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220303222432297.png)

   1. 请求行:请求方式(get/post)、URL 和 HTTP 协议版本 3 个部分组成
   2. 请求头部:描述客户端的基本信息，从而把客户端相关的信息告知服务器
      1. 由多行 键/值对 组成
      2. ![image-20220303222714365](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220303222714365.png)
   3. 空行:通知服务器请求头部至此结束
   4. 请求体:要通过 POST 方式提交到服务器的数据(==get请求没有请求体==)



### HTTP响应消息

1. 响应消息就是服务器响应给客户端的消息内容

2. 组成:状态行、响应头部、空行 和 响应体

   ![image-20220303223208426](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220303223208426.png)

   1. 状态行:HTTP 协议版本、状态码和状态码的描述文本
   2. 相应头部:描述服务器的基本信息。响应头部由多行 键/值对 组成
   3. 空行:用来通知客户端响应头部至此结束
   4. 响应体:服务器响应给客户端的资源内容





### HTTP请求方法:

![image-20220303223523665](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220303223523665.png)





### HTTP响应状态码

1. 分为5类:

   ![image-20220303223655141](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220303223655141.png)

2.  2** 成功相关

   | 状态码 | 英文    | 中文描述 |
   | ------ | ------- | -------- |
   | 200    | OK      | 请求成功 |
   | 201    | Created | 已创建   |

3.  3** 重定向相关

   | 状态码 | 英文              | 中文描述                                                     |
   | ------ | ----------------- | ------------------------------------------------------------ |
   | 301    | Moved Permanently | 永久移动。请求的资源已被永久的移动到新URL，返回信息会包括新的URL |
   | 302    | Found             | 临时移动                                                     |
   | 304    | Not Modified      | 未修改。所请求的资源未修改，服务器返回此状态码时，不会返回任何资源（响应消息中不包含响应体）.==客户端通常会缓存访问过的资源== |

4.  4**客户端错误相关

   | 状态码 | 英文            | 中文描述                                                     |
   | ------ | --------------- | ------------------------------------------------------------ |
   | 400    | Bad Request     | 1、语义有误，当前请求无法被服务器理解。除非进行修改，否则客户端不应该重复提交这个请求。2、请求参数有误。 |
   | 401    | Unauthorized    | 当前请求需要用户验证(接口不是人人可以用的情况)               |
   | 403    | Forbidden       | 服务器已经理解请求，但是拒绝执行它。                         |
   | 404    | Not Found       | 服务器无法根据客户端的请求找到资源（网页）。                 |
   | 408    | Request Timeout | 请求超时                                                     |

5.  5**服务端错误相关

   | 状态码 | 英文                 | 中文描述                             |
   | ------ | -------------------- | ------------------------------------ |
   | 500    | Internal ServerError | 服务器内部错误                       |
   | 501    | Not Implemented      | 服务器不支持该请求方法，无法完成请求 |
   | 503    | Service Unavailable  | 由于超载或系统维护                   |
