# NodeJS

## day1

### 初识Node.JS

1. 浏览器JS解析引擎
   1. Chrome 浏览器 => V8
   2. Firefox 浏览器=> OdinMonkey（奥丁猴）
   3. Safri 浏览器=> JSCore
   4. IE 浏览器=> Chakra（查克拉）
2. Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行环境。
3. 区分 LTS 版本和 Current 版本
   1. LTS 为长期稳定版，对于追求稳定性的企业级项目来说，推荐安装 LTS 版本的 Node.js。
   2. Current 为新特性尝鲜版，对热衷于尝试新特性的用户来说，推荐安装 Current 版本的 Node.js。





### fs模块

1. 使用``require('fs')``导入模块
2. fs.readFile() 
   1. ```fs.readFile(path,options,callback) ```
   2. 参数1：必选参数，字符串，表示文件的路径。
   3. 参数2：可选参数，表示以什么编码格式来读取文件。
   4. 参数3：必选参数，文件读取完成后，通过回调函数拿到读取的结果。
3. fs.writeFile()
   1. ```fs.writeFile(file, data[, options], callback)```
   2. 参数1：必选参数，需要指定一个文件路径的字符串，表示文件的存放路径。
   3. 参数2：必选参数，表示要写入的内容。
   4. 参数3：可选参数，表示以什么格式写入文件内容，默认值是 utf8。
   5. 参数4：必选参数，文件写入完成后的回调函数
   6. ==只会创建文件,不会创建路径==
   7. ==新内容会覆盖文件中旧内容==
4. 路径动态拼接错误
   1. 如果提供的操作路径是以 ./ 或 ../ 开头的相对路径时，很容易出现路径动态拼接错误的问题。
   2. 解决方案：==在使用 fs 模块操作文件时，直接提供完整的路径==，不要提供 ./ 或 ../ 开头的相对路径，从而防止路径动态拼接的问题。
   3. 使用```__dirname```表示当前文件所处的目录



### path模块

1. path 模块是 Node.js 官方提供的、用来处理路径的模块。
2. 路径拼接
   1. ```path.join([...paths])```
   2. paths <string> 路径片段的序列
   3. 返回值: <string>
   4. ==..\ 会抵消前面的路径==,  .\没有
   5. 今后凡是涉及到路径拼接的操作，都要使用 path.join() 方法进行处理。不要直接使用 + 进行字符串的拼接。
3. 获取路径中的文件名
   1. ```path.basename(path[, ext]) ```
   2. path <string> 必选参数，表示一个路径的字符串
   3.  ext <string> 可选参数，表示文件扩展名
   4. 返回: <string> 表示路径中的最后一部分
4. 获取路径中的文件扩展名
   1.  ```path.extname(fpath) ```
   2. path <string>必选参数，表示一个路径的字符串
   3. 返回: <string> 返回得到的扩展名字符串





### HTTP模块

1. 基于 Node.js 提供的http 模块，通过几行简单的代码，就能轻松的手写一个服务器软件，从而对外提供 web 服务

2. 服务器相关概念

   1. IP地址

      1. 地址就是互联网上每台计算机的唯一地址
      2. 用“点分十进制”表示成（a.b.c.d）的形式，其中，a,b,c,d 都是 0~255 之间的十进制整数
      3. 在开发期间，自己的电脑既是一台服务器，也是一个客户端，为了方便测试，可以==在自己的浏览器中输入 127.0.0.1 这个IP 地址==，就能把自己的电脑当做一台服务器进行访问了

   2. 域名和域名服务器

      1. 在开发测试期间，==127.0.0.1 对应的域名是 localhost==，它们都代表我们自己的这台电脑，在使用效果上没有任何区别。

   3. 端口号

      1. 每个 web 服务都对应一个唯一的端口号。客户端发送过来的网络请求，通过端口号，可以被准确地交给对应的 web 服务进行处理

         ![image-20220305162607047](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220305162607047.png)

      2. 每个端口号不能同时被多个 web 服务占用
      3. ==URL 中的 80 端口可以被省略==

3. 创建web服务器

   1. 导入:```1 const http = require('http')```

   2. 创建实例:```const server =http.createServer() ```

   3. 为服务器实例绑定 request 事件

      ```javascript
      1／／ 使用服务器实例的．on（）方法，为服务器绑定一个 request 事件
      
      server.on('request', (req, res) => {
          
       ／／只要有客户端来请求我们自己的服务器，就会触发 request 事件，从而调用这个事件处理函数
       
       console.log('Someone visit our web server.')
      })
      ```

   4. 启动服务器:

      ```js
      ／／调用 server．listen（端口号，cb回调）方法，即可启动 web 服务器2 server.listen(80, () =>{
          
       console.log('http server running at http://127.0.0.1')
      
      })
      ```

4. req请求对象(包含了客户端请求的信息)

   1. 只要服务器接收到了客户端的请求，就会调用通过 server.on() 为服务器绑定的 request 事件处理函数

      ![image-20220305164453372](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220305164453372.png)

   2. req.url:客户端请求的URL地址

   3. req.method:客户端method请求类型

5. res 响应对象(让服务器端返回给客户端内容)

   1. 如果想访问与服务器相关的数据或属性

      ![image-20220305164758758](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220305164758758.png)

   2. 解决中文乱码

      ![image-20220305170146680](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220305170146680.png)

6. 根据不同的 url 响应不同的 html 内容

   1. 步骤:![image-20220305170307791](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220305170307791.png)
   2. 动态响应:![image-20220305170442749](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220305170442749.png)





## day2

### 模块化

1. 模块化是指解决一个复杂问题时，自顶向下逐层把系统划分成若干模块的过程。对于整个系统来说，模块是可组合、分解和更换的单元。

2. Node.JS模块分类

   1. 内置模块（内置模块是由 Node.js 官方提供的，例如 fs、path、http 等）
   2. 自定义模块（用户创建的每个 .js 文件，都是自定义模块）
   3. 第三方模块（由第三方开发出来的模块，并非官方提供的内置模块，也不是用户创建的自定义模块，使用前需要先下载）
   4. 加载模块:![image-20220305172352065](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220305172352065.png)
   5. ==使用 require() 方法加载其它模块时，会执行被加载模块中的代码。==

3. 模块作用域

   1. 和函数作用域类似，==只能在当前模块内被访问==，这种模块级别的访问限制，叫做模块作用域。

4. module 对象

   1. 在每个 .js 自定义模块中都有一个 module 对象，它里面存储了和当前模块有关的信息

      ![image-20220305172740588](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220305172740588.png)

   2. model.exports对象

      1. 可以使用 module.exports 对象，将模块内的成员共享出去，供外界使用

      2. 外界用 require() 方法导入自定义模块时，得到的就是 module.exports 所指向的对象。

      3. 在对象的前面加上module.exports,使module.exports挂载指定的对象

         ![image-20220305173431066](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220305173431066.png)

      4. ==导入的结果，永远以 module.exports 指向的对象为准。==
         1. 使用model.exports指向新对象时,旧对象不会在被指向

      5. ==Node 提供了 exports 对象。==

         1. 默认情况下，exports 和 module.exports 指向同一个对象
         2. 最终共享的结果，还是以 module.exports 指向的对象为准。

      6. 

      7. 使用误区:

         1. ![image-20220305193704498](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220305193704498.png)
         2. 因为属性没有冲突

      8. ==为了防止混乱，建议大家不要在同一个模块中同时使用 exports 和 module.exports==

5. Node.js 遵循了 CommonJS 模块化规范，CommonJS 规定了模块的特性和各模块之间如何相互依赖。

   1. CommonJS 规定：
      * 每个模块内部，module 变量代表当前模块。
      * module 变量是一个对象，它的 exports 属性（即 module.exports）是对外的接口。
      * 加载某个模块，其实是加载该模块的 module.exports 属性。require() 方法用于加载模块





### npm与包

1. Node.js 中的第三方模块又叫做包。
2. 使用```npm install 包的名称@版本号```来安装包
3. node_modules 文件夹用来存放所有已安装到项目中的包。require() 导入第三方包时，就是从这个目录中查找并加载包。
4. package-lock.json 配置文件用来记录 node_modules 目录下的每一个包的下载信息，例如包的名字、版本号、下载地址等。
5. 版本号
   1. 第1位数字：大版本
   2. 第2位数字：功能版本
   3. 第3位数字：Bug修复版本
6. npm 规定，在项目根目录中，必须提供一个叫做 package.json 的包管理配置文件。用来记录与项目有关的一些配置信息。
   * 项目的名称、版本号、描述等
   * 项目中都用到了哪些包
   * 哪些包只在开发期间会用到
   * 那些包在开发和部署时都需要用到
7. ==今后在项目开发中，一定要把 node_modules 文件夹，添加到 .gitignore 忽略文件中。==
8. 运行 npm install 命令（或 npm i）一次性安装所有的依赖包
9. devDependencies 节点
   1. 如果某些包只在项目开发阶段会用到，在项目上线之后不会用到，则建议把这些包记录到 devDependencies 节点中。
   2. 与之对应的，如果某些包在开发和项目上线之后都需要用到，则建议把这些包记录到 dependencies 节点中
   3. 使用:```npm install 包名 -D```把包记录到 devDependencies 节点中
10. 包的分类
    1.  项目包和全局包
    2. 项目包分为两类
       1. 开发依赖包（被记录到 devDependencies 节点中的包，只在开发期间会用到）
       2. 核心依赖包（被记录到 dependencies 节点中的包，在开发期间和项目上线之后都会用到）
    3. 全局包
       1. 只有工具性质的包，才有全局安装的必要性。因为它们提供了好用的终端命令。
       2. 判断某个包是否需要全局安装后才能使用，可以参考官方提供的使用说明即可
    4. 规范的包
       1. 包必须以单独的目录而存在
       2. 包的顶级目录下要必须包含 package.json 这个包管理配置文件
       3. package.json 中必须包含 name，version，main 这三个属性，分别代表包的名字、版本号、包的入口。
    5. ==在```exports```中,使用```...```来表示展开运算符,将属性展开交给新对象==



### 模块加载机制

1. 优先从缓存中加载
   1. 不论是内置模块、用户自定义模块、还是第三方模块，它们都会优先从缓存中加载，从而提高模块的加载效率。
2. 使用 require() 加载自定义模块时，必须指定以 ./ 或 ../ 开头的路径标识符。在加载自定义模块时，如果没有指定 ./ 或 ../这样的路径标识符，则 node 会把它当作内置模块或第三方模块进行加载。
3. 如果省略了文件的扩展名，则 Node.js 会按顺序分别尝试加载以下的文件：
   1. 按照确切的文件名进行加载
   2. 补全 .js 扩展名进行加载
   3. 补全 .json 扩展名进行加载
   4. 补全 .node 扩展名进行加载
   5. 加载失败，终端报错

4. 第三方模块的加载机制
   1. 如果没有找到对应的第三方模块，则移动到再上一层父目录中，进行加载，直到文件系统的根目录。
5. 目录作为模块
   1. 在被加载的目录下查找一个叫做 package.json 的文件，并寻找 main 属性，作为 require() 加载的入口
   2. 如果目录里没有 package.json 文件，或者 main 入口不存在或无法解析，则 Node.js 将会试图加载目录下的 index.js 文件。
   3. 如果以上两步都失败了，则 Node.js 会在终端打印错误消息，报告模块的缺失：Error: Cannot find module 'xxx'



## day3 Express

### 初始Express

1. Express 的作用和 Node.js 内置的 http 模块类似，是专门用来创建 Web 服务器的。

2. Express 的本质：就是一个 npm 上的第三方包，提供了快速创建 Web 服务器的便捷方法。

3. 使用 Express，我们可以方便、快速的创建 Web 网站的服务器或 API 接口的服务器。

4. 基本使用

   ```JavaScript
   const express=require('express')
   
   const app=express()
   
   app.listen(80 ,()=>{
       console.log('express server running');
   })
   ```

5. 监听GET请求

   1. ```app.get(`请求URL, function（req，res）｛／＊处理函数＊／}）```

6. 监听POST请求

   1. ```app.post(`请求URL, function（req，res）｛／＊处理函数＊／}）```

7. 获取 URL 中的动态参数

   1. 通过 req.params 对象，可以访问到 URL 中，通过 : 匹配到的动态参数：
   2. 动态匹配:![image-20220305210352308](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220305210352308.png)

8. 托管静态资源

   1. 通过它，我们可以非常方便地创建一个静态资源服务器，

   2. 示例:通过如下代码就可以将 public 目录下的图片、CSS 文件JavaScript 文件对外开放访问了：

      ![image-20220305210437231](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220305210437231.png)

   3. 存放静态文件的目录名不会出现在 URL 中。
   4. 访问静态资源文件时，express.static() 函数会根据目录的添加顺序查找所需的文件。
   5. 挂载路径前缀
      1. ![image-20220305210825312](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220305210825312.png)

9. 使用nodemon:它能够监听项目文件的变动，当代码被修改后nodemon 会自动帮我们重启项目，极大方便了开发和调试.





### Express路由

1. 路由:广义上来讲，路由就是映射关系。

   1. 在 Express 中，路由指的是==客户端的请求==与==服务器处理函数==之间的映射关系。

2. 匹配过程

   ![image-20220305211730629](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220305211730629.png)

   1. 按照定义的先后顺序进行匹配
   2. 请求类型和请求的URL同时匹配成功，
      才会调用对应的处理函数

3. 模块化路由

   1. 创建路由模块对应的 .js 文件

   2. 调用 express.Router() 函数创建路由对象

   3. 向路由对象上挂载具体的路由

   4. 使用 module.exports 向外共享路由对象

   5. 使用 app.use() 函数注册路由模块

      ![image-20220305212105133](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220305212105133.png)

   6. 注册路由模块

      ![image-20220305212308647](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220305212308647.png)

      1. app.use()作用:注册全局中间件

   7. 为路由模块添加前缀

      1. ![image-20220305212604374](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220305212604374.png)





### express中间件

1. 中间件（Middleware ）:特指业务流程的中间处理环节。

2. Express 中间件的格式

   1. 本质上就是一个 function 处理函数

      ![image-20220305212810952](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220305212810952.png)

      * 中间件函数的形参列表中，必须包含 next 参数。而路由处理函数中只包含 req 和 res

3. next函数作用

   1. next 函数是实现多个中间件连续调用的关键，它表示把流转关系转交给下一个中间件或路由。

      ![image-20220305212907110](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220305212907110.png)

4. 定义中间件函数

   1. ![image-20220305212953023](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220305212953023.png)

5. 全局生效的中间件

   1. 客户端发起的任何请求，到达服务器之后，都会触发的中间件，叫做全局生效的中间件。

   2. app.use(中间件函数)，即可定义一个全局生效的中间件

      ![image-20220305213133999](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220305213133999.png)

      ```js
      const app=express()
      const mw=function(req,res,next){
          console.log("中间件")
          next()
      }
      app.use(mw)
      app.get('/',(req,res)=>{
          res.send("home page")
          console.log("home page")
      })
      app.listen(80 ,()=>{
          console.log('express server running');
      })
      ```

      * 先打印中间件,在打印home page

      * 简化

        ![image-20220305213844227](../../../AppData/Roaming/Typora/typora-user-images/image-20220305213844227.png)

6. 中间件的作用

   1. 多个中间件之间，==共享同一份 req 和 res。==
   2. 基于这样的特性，我们可以在上游的中间件中，统一为 req 或 res 对象添加自定义的属性或方法，供下游的中间件或路由进行使用。
   3. 示例:在上游挂载到达时间这个自定义属性(req.starttime),供下游使用
      * 如果不用中间件,获得时间的代码要在每个路由中写一份

7. 局部中间件

   1. 不使用 app.use() 定义的中间件，叫做局部生效的中间件

      ![image-20220305214334850](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220305214334850.png)

      (中间件mw1只在第一个路由中生效)

   2. 定义多个局部中间件

      ![image-20220305214514193](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220305214514193.png)



8. 注意事项

   1. 一定要在==路由之前==注册中间件
   2. 客户端发送过来的请求，可以连续调用多个中间件进行处理
   3. 执行完中间件的业务代码之后，不要忘记调用 next() 函数
   4. 为了防止代码逻辑混乱，调用 next() 函数后不要再写额外的代码
   5. 连续调用多个中间件时，==多个中间件之间，共享 req 和 res 对象==

9. 中间件分类

   1. 应用级别中间件:绑定到 app 实例上的中间件，叫做应用级别的中间件

   2. 路由级别的中间件:绑定到 express.Router() 实例上的中间件，叫做路由级别的中间件。

   3. 错误级别的中间件:错误级别中间件的作用：专门用来捕获整个项目中发生的异常错误，从而防止项目异常崩溃的问题。

      1. ==除了错误级别的中间件,其他中间件要在路由前配置==

      ![image-20220305215014561](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220305215014561.png)

   4. Express内置的中间件:

      1. express.static 快速托管静态资源的内置中间件，例如： HTML 文件、图片、CSS 样式等（无兼容性）

      2. express.json 解析 JSON 格式的请求体数据（有兼容性，仅在 4.16.0+ 版本中可用）

      3. express.urlencoded 解析 URL-encoded 格式的请求体数据（有兼容性，仅在 4.16.0+ 版本中可用

         ![image-20220305215502125](../../../AppData/Roaming/Typora/typora-user-images/image-20220305215502125.png)

   5. 第三方中间件

      1. 则客户端会把数据切割后，分批发送到服务器。所以 data 事件可能会触发多次，每一次触发 data 事件时，获取到数据只是完整数据的一部分

         ![image-20220305220722784](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220305220722784.png)





### express接口

1. 创建API路由模块

   ![image-20220306155340611](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220306155340611.png)

2. 编写GET和POST接口

![image-20220306155232204](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220306155232204.png)

![image-20220306161052224](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220306161052224.png)





3. 接口的跨域问题
   1. 解决接口跨域问题的方案主要有两种：
      1. CORS（主流的解决方案，推荐使用）
      2. JSONP（有缺陷的解决方案：只支持 GET 请求）
4. cors 中间件
   1. 使用步骤
      1. 运行 npm install cors 安装中间件
      2. 使用 const cors = require('cors') 导入中间件
      3. 在路由之前调用 app.use(cors()) 配置中间件
5. 什么是CORS
   1. CORS （Cross-Origin Resource Sharing，跨域资源共享）由一系列 HTTP 响应头组成，这些 HTTP 响应头决定浏览器是否阻止前端 JS 代码跨域获取资源。
   2. CORS 主要在服务器端进行配置。客户端浏览器无须做任何额外的配置，即可请求开启了 CORS 的接口。
   3.  CORS 在浏览器中有兼容性。只有支持 XMLHttpRequest Level2 的浏览器，才能正常访问开启了 CORS 的服务端接口（例如：IE10+、Chrome4+、FireFox3.5+）。
6. CORS响应头部
   1. Access-Control-Allow-Origin:
      1. 示例:例如，下面的字段值将只允许来自http://itcast.cn 的请求：![image-20220306163002379](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220306163002379.png)
   2. Access-Control-Allow-Headers
      1. 默认情况下，CORS 仅支持客户端向服务器发送如下的 9 个请求头
   3. Access-Control-Allow-Methods
      1. 如果客户端希望通过 PUT、DELETE 等方式请求服务器的资源，则需要在服务器端，通过 Access-Control-Alow-Methods来指明实际请求所允许使用的 HTTP 方法。
7. CORS请求的分类
   1. 简单请求
      1. 请求方式：GET、POST、HEAD 三者之一
      2. HTTP 头部信息不超过以下几种字段
   2. 预检请求
      1. 请求方式为 GET、POST、HEAD 之外的请求 Method 类型
      2. 请求头中包含自定义头部字段
      3. 向服务器发送了 application/json 格式的数据
      4. ==客户端与服务器之间会发生两次请求，OPTION 预检请求成功之后，才会发起真正的请求==
8. JSONP 接口
   1. 如果项目中已经配置了 CORS 跨域资源共享，为了防止冲突，必须在配置 CORS 中间件之前声明 JSONP 的接口。否则JSONP 接口会被处理成开启了 CORS 的接口
   2. ![image-20220306164342393](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220306164342393.png)







### day3 数据库

### 基础

1. 常见数据库种类
   1. MySQL 数据库（目前使用最广泛、流行度最高的开源免费数据库；Community + Enterprise）
   2. Oracle 数据库（收费）
   3. SQL Server 数据库（收费）
   4. Mongodb 数据库（Community + Enterprise）

2. MySQL
   1. MySQL Server：专门用来提供数据存储和服务的软件。
   2. MySQL Workbench：可视化的 MySQL 管理工具，通过它，可以方便的操作存储在 MySQL Server 中的数据。

3. 创建数据表
   1. ![image-20220306171905770](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220306171905770.png)

4. SQL语法

   1. WHERE子句:![image-20220306175351127](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220306175351127.png)

   2. 排序

      1. ORDER BY 语句用于根据指定的列对结果集进行排序。

      2. 如果您希望按照降序对记录进行排序，可以使用 DESC 关键字。(DESC在后面添加)

      3. 对 users 表中的数据，先按照 status 字段进行降序排序，再按照 username 的字母顺序，进行升序排序，示例如下

         ![image-20220306175602842](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220306175602842.png)

   3. COUNT(*)

      1. COUNT(*) 函数用于返回查询结果的总数据条数，语法格式如下：

         ![image-20220306175644087](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220306175644087.png)

   4. 使用 AS 为列设置别名

      1. 如果希望给查询出来的列名称设置别名，可以使用 AS 关键字，示例如下

         ![image-20220306175731742](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220306175731742.png)



### 在项目操作MySQL

1. 配置和检查

   ```js
   const mysql  = require('mysql')
   
   const db_ = mysql.createPool({
       host: 'localhost',
       user: 'root',
       password: 'admin123',
       database: 'my_db_01'
   })
   db_.query('SELECT 1', (err, result) => {
       if (err) {return console.error(err.message)}
       console.log(result)
   })
   ```

2. 插入数据

   ![image-20220306182732219](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220306182732219.png)

   ![image-20220306182818369](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220306182818369.png)

3. 更新数据

   ![image-20220306183235572](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220306183235572.png)

4. 删除数据

   1. 为了保险起见，推荐使用标记删除的形式，来模拟删除的动作。所谓的标记删除，就是在表中设置类似于 status 这样的状态字段，来标记当前这条数据是否被删除。

   ![image-20220306183257062](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220306183257062.png)







### 前后端身份认证

### 基础

1. 服务端渲染的 Web 开发模式

   1. 服务器发送给客户端的 HTML 页面，是在服务器通过字符串的拼接，动态生成的。

      ![image-20220306183736024](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220306183736024.png)

   2. 缺点:
      1. 占用服务器端资源。即服务器端完成 HTML 页面内容的拼接，如果请求较多，会对服务器造成一定的访问压力。
      2. 不利于前后端分离，开发效率低。使用服务器端渲染，则无法进行分工合作，尤其对于前端复杂度高的项目，不利于项目高效开发。

2. 前后端分离的 Web 开发模式
   1. 开发体验好。前端专注于 UI 页面的开发，后端专注于api 的开发，且前端有更多的选择性。
   2. 用户体验好。Ajax 技术的广泛应用，极大的提高了用户的体验，可以轻松实现页面的局部刷新。
   3. 减轻了服务器端的渲染压力。因为页面最终是在每个用户的浏览器中生成的。
3. 身份认证
   1. 服务端渲染推荐使用 Session 认证机制
   2. 前后端分离推荐使用 JWT 认证机制



### Session认证机制

1. 无状态性:HTTP 协议的无状态性，指的是客户端的每次 HTTP 请求都是独立的，连续多个请求之间没有直接的关系，==服务器不会主动保留每次 HTTP 请求的状态。==

2. 如何突破 HTTP 无状态的限制:对于超市来说，为了方便收银员在进行结算时给 VIP 用户打折，超市可以为每个 VIP 用户发放会员卡

3. Cookie :存储在用户浏览器中的一段不超过 4 KB 的字符串。它由一个名称（Name）、一个值（Value）和其它几个用于控制 Cookie 有效期、安全性、使用范围的可选属性组成。

   1. cookie不具有安全性
   2. 特性:自动发送  域名独立  过期时限  4KB 限制

4. seesion认证机制

   ![image-20220306184956084](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220306184956084.png)

5. 在 Express 中使用 Session 认证

   1. 配置Session

      ![image-20220306190014317](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220306190014317.png)

   2. 向session存数据

      ![image-20220306190641304](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220306190641304.png)

   3. 向session取数据

      ![image-20220306190658854](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220306190658854.png)

   4. 清空session

      ![image-20220306190750054](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220306190750054.png)



### JWT认证机制

1. JWT（英文全称：JSON Web Token）是目前最流行的跨域认证解决方案

2. 工作原理:

   ![image-20220306191029585](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220306191029585.png)

3. 组成部分

   1. 分别是 Header（头部）、Payload（有效荷载）、Signature（签名）

   2. Payload 部分才是真正的用户信息，它是用户信息经过加密之后生成的字符串。Header 和 Signature 是安全性相关的部分，只是为了保证 Token 的安全性。

      ![image-20220306191258531](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220306191258531.png)

4. 使用JWT

   1. 安装两个包

      * jsonwebtoken 用于生成 JWT 字符串
      * express-jwt 用于将 JWT 字符串解析还原成 JSON 对象

   2. 定义secret密钥

      1. 为了保证 JWT 字符串的安全性，防止 JWT 字符串在网络传输过程中被别人破解，我们需要专门定义一个用于加密和解密的 secret 密钥
      2. secret密钥本质:一个自定义的字符串

   3. 生成JWT字符串

      ![image-20220306191911412](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220306191911412.png)

   4. 将 JWT 字符串还原为 JSON 对象

      ![image-20220306192105309](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220306192105309.png)

      1. 密码不要加密到token中

   5. 使用 req.user 获取用户信息

      1. ![image-20220306193106868](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220306193106868.png)

      2. 只要token解析成功,就会自动将信息挂载到req.user中

      3. express错误中间件

         1. 在所有的中间件的最后注册
         2. ![image-20220306193257918](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220306193257918.png)

         
