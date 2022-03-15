# VUE2

## Webpack

### 前端工程化

1. 在企业级的前端项目开发中，把前端开发所需的工具、技术、流程、经验等进行规范化、标准化。
2. 目前主流的前端工程化解决方案：
   * webpack（ https://www.webpackjs.com/ ）
   * parcel（ https://zh.parceljs.org/ ）
3. 实际的前端开发：
   * 模块化（js 的模块化、css 的模块化、资源的模块化）
   * 组件化（复用现有的 UI 结构、样式、行为）
   * 规范化（目录结构的划分、编码规范化、接口规范化、文档规范化、 Git 分支管理）
   * 自动化（自动化构建、自动部署、自动化测试）

### webpack基本使用

1. 功能:它提供了友好的前端模块化开发支持，以及代码压缩混淆、处理浏览器端 JavaScript 的兼容性、性能优化等强大的功能

2. 配置webpack
   
   1. 安装
   
   ```bash
   npm install webpack@5.42.1 webpack-cli@4.7.2 -D
   ```
   
   2. 在项目中配置webpack
      
      1. 在项目根目录中，创建名为 webpack.config.js 的 webpack 配置文件，并初始化如下
         
         ![image-20220307112646320](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220307112646320.png)
      
      2. 在package.json的script节点下,新增dev脚本如下
         
         ![image-20220307112957569](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220307112957569.png)
      
      3. 运行```npm run dev ```命令

3. mode的可选值
   
   1. development:不压缩
   2. production:压缩

4. 自定义打包的入口与出口
   
   1. 在 webpack 4.x 和 5.x 的版本中，有如下的默认约定：
      
      * 默认的打包入口文件为 src -> index.js
      * 默认的输出文件路径为 dist -> main.js
   
   2. 在 webpack.config.js 配置文件中，通过 entry 节点指定打包的入口。通过 output 节点指定打包的出口。示例代码如下：
      
      ![image-20220307152029618](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220307152029618.png)

### webpack中的插件

1. webpack-dev-server
   
   1. 类似于 node.js 阶段用到的 nodemon 工具
   2. ```npm i webpack-dev-server@3.11.2 -D```
   3. ==配置了 webpack-dev-server 之后，打包生成的文件存放到了内存中==
      1. 提高了实时打包输出的性能，因为内存比物理磁盘速度快很多
      2. 修改index.html,使用内存中的main.js

2. html-webpack-plugin
   
   1. 将 src 目录下的 index.html 首页，复制到项目根目录中一份！不用打开scr目录就可看到效果
   
   2. 安装:```npm install html-webpack-plugin@5.3.2 -D```
   
   3. 配置:![image-20220307154916135](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220307154916135.png)
   
   4. 会自动添加一个脚本,应用内存中的脚本
   
   5. 自动打开浏览器
      
      ![image-20220307155838871](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220307155838871.png)

### webpack的loader

1. 需要loader加载器来打包非.js的模块
   
   ![image-20220307160435818](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220307160435818.png)

2. 打包css文件
   
   1. 安装:```npm i style-loader@3.0.0 css-loader@5.2.6 -D ```
   
   2. 在module -> rules 数组中，添加 loader 规则.
      
      ![image-20220307161042504](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220307161042504.png)
   
   3. 处理过程
      
      1. webpack发现文件处理不了时,查找配置文件中的数组,查看是否配置了loader加载器
      2. 先将文件交给最后一个loader:css-loader处理,然后交给style-loader处理
      3. 将处理的结果移交给目标的js文件.生成打包的文件

3. 打包less文件
   
   1. 安装:```npm i less-loader@10.0.1 less@4.1.1 -D```
   2. ![image-20220307161736473](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220307161736473.png)

4. base64图片
   
   1. 可以防止发起一些不必要的请求
   2. 只适合体积小的logo等图片

5. 打包url路径相关的文件(图片)
   
   1. 安装:``` npm i url-loader@4.1.1 file-loader@6.2.0 -D```
   2. ![image-20220307162714133](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220307162714133.png)
      * limit用来指定图片的大小,小于limit时会被转为base64格式的图片

6. 打包js的高级语法
   
   1. 安装:```npm i babel-loader@8.2.2 @babel/core@7.14.6 @babel/plugin-proposal-decorators@7.14.5 -D```
   
   2. 添加规则:![image-20220307163747664](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220307163747664.png)
      
      * exclude:排除第三方包
   
   3. 配置babel-loader
      
      ![image-20220307164031927](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220307164031927.png)

### 打包发布

1. 配置webpack
   
   1. 在 package.json 文件的 scripts 节点下，新增 build 命令如下：
      
      ![image-20220307164843699](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220307164843699.png)

2. 把图片文件放到image目录中
   
   ![image-20220307195227957](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220307195227957.png)

3. 自动清理dist文件夹
   
   ![image-20220307195741301](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220307195741301.png)

### Source Map

1. Source Map 文件中存储着压缩混淆后的代码，所对应的转换前的位置。

2. 在webpack.config.js的```module.exports```中设置devtool的值为```‘eval-source-map’```

3. 为了防止源代码泄露,可以设置devtool的值为```nonsource-source-map```

4. 建议使用@表示源代码目录,从外向里找.不建议使用../从里向外找
   
   1. @需要先配置.在webpack.config.js中添加如下
      
      ![image-20220307201247260](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220307201247260.png)

## Vue基础

1. 特性
   
   1. 数据驱动视图
      
      1. vue 会监听数据的变化，从而自动重新渲染页面的结构。
      
      ![image-20220307202059362](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220307202059362.png)
   
   2. 双向数据绑定
      
      1. > form表单负责采集数据,ajax负责提交数据
      
      2. 双向数据绑定可以辅助开发者在不操作 DOM 的前提下，自动把用户填写的内容同步到数据源中。示意图如下：
         
         ![image-20220307202600578](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220307202600578.png)

### Vue的指令和过滤器

#### 内容渲染指令

* v-text
* {{ }}
* v-html
1. v-text
   1. ![image-20220307205316984](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220307205316984.png)
   2. 会覆盖元素默认的值,所以在实际中那个,{{}}会更为常用
2. v-html
   1. 如果要==把包含 HTML 标签的字符串渲染为页面的 HTML 元素==
3. el不要绑定标签,否则只处理第一个

属性绑定指令

1. 插值表达式不能用在属性节点,只能用在内容节点

2. v-bind(简写为:)
   
   ![image-20220307210817918](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220307210817918.png)

3. 模板渲染语法中，除了支持绑定简单的数据值之外，还支持 Javascript 表达式的运算
   
   ![image-20220307210951431](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220307210951431.png)
   
   1. v-bind绑定属性期间,如果要动态拼接,需要在字符串的外面添加单引号

#### 事件绑定指令(简写为 @)

1. 在DOM中绑定
   
   ![image-20220307211845601](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220307211845601.png)

2. 在methods节点内定义(this.count也可以写成vm.count)
   
   ![image-20220307211756024](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220307211756024.png)

3. 可以给事件处理函数设定形参,然后在绑定事件函数的时候输入参数(```@click=“addcount(2)”```)

4. 原生对象的```onclick,oninput,onkeyup```需要改为```v-on:click、v-on:input、v-on:keyup```

#### 事件对象$event

1. $event 是 vue 提供的特殊变量，用来表示原生的事件参数对象 event
   
   ![image-20220307213602396](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220307213602396.png)
   
   1. 使用场景:调用函数需要传参且同时需要保留原来的事件对象

#### 事件修饰符

1. 如果需要调用event.preventDefault() 或 event.stopPropagation()阻止默认行为,可以使用vue的事件修饰符
   
   ![image-20220307214736449](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220307214736449.png)
   
   ![image-20220307214747351](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220307214747351.png)

#### 按键修饰符

1. 可以为键盘相关的事件添加按键修饰符，例如：
   
   ![image-20220307215036715](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220307215036715.png)

#### 双向数据绑定指令

1. v-model:用来辅助开发者在不操作 DOM 的前提下，快速获取表单的数据。
   
   ![image-20220307215747580](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220307215747580.png)
   
   可以实现输入框的内容变化时,文本和data的内容也发生变化

2. v-model指令可以和input textarea select等表单元素使用

3. v-model修饰符
   
   ![image-20220307220220646](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220307220220646.png)
   
   1. 懒更新:只会在输入完结果时更新值,不会实时同步

#### 条件渲染指令

1. v-if 指令会动态地创建或移除 DOM 元素，从而控制元素在页面上的显示与隐藏；

2. v-show 指令会动态为元素添加或移除 style="display: none;" 样式，从而控制元素的显示与隐藏；

3. 如果需要非常频繁地切换，则使用 v-show 较好.如果在运行时条件很少改变，则使用 v-if 较好

4. ![image-20220307221218691](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220307221218691.png)

#### 列表渲染指令

1. ![image-20220307221550519](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220307221550519.png)
2. key的注意事项
   1. key 的值只能是字符串或数字类型
   2. key 的值必须具有唯一性（即：key 的值不能重复）
   3. 建议把数据项 id 属性的值作为 key 的值（因为 id 属性的值具有唯一性）
   4. 使用 index 的值当作 key 的值没有任何意义（因为 index 的值不具有唯一性）
   5. 建议使用 v-for 指令时一定要指定 key 的值（既提升性能、又防止列表状态紊乱

#### 过滤器

1. 过滤器（Filters）是 vue 为开发者提供的功能，常用于文本的格式化。

2. 实例
   
   ![image-20220308171535562](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220308171535562.png)

3. 定义
   
   ![image-20220308172015606](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220308172015606.png)
   
   1. 使用形参可以得到message的值
   2. 一定要有return返回值

4. 全局过滤器
   
   ![image-20220308174459082](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220308174459082.png)
   
   1. 如果名字冲突,私有的过滤器的优先级大于全局过滤器

5. 过滤器传参
   
   1. ![image-20220308175225600](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220308175225600.png)
   2. 第一个的位置已经被固定

### 侦听器

#### 方法格式侦听器

1. 允许开发者监听数据的变化,从而进行操作
   
   ![image-20220309172421572](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220309172421572.png)

2. 所有的监听器定义到watch上,本质上是一个函数watch

3. 案例:使用watch检测用户名是否占用
   
   ![image-20220309172844823](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220309172844823.png)

4. 在刚进入的时候,不会立即触发

5. 侦听器是一个对象,如果只是属性发生变化,不会触发侦听器

#### 对象格式监听器

1. 使用```immediate```选项来触发

2. ![image-20220309174332007](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220309174332007.png)

3. 可以使用deep选项,监听对象的属性的变化

4. 监听子属性的变化,包裹一层单引号

### 计算属性

1. 计算属性指的是通过一系列运算之后，最终得到一个属性值。
   
   ![image-20220309175354959](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220309175354959.png)

2. 场景:不使用的话需要先使用v-model双向监听,在使用模板字符串进行拼接.

3. 所有的计算属性定义到```computed```属性==之下==

4. 使用的时候作为属性使用即可

5. 使用的属性的值发生变化,计算属性会被重新赋值

### axios 的基本使用

1. 发起 GET 请求：
   
   ```js
   axios({
     // 请求方式
     method: 'GET',
     // 请求的地址
     url: 'http://www.liulongbin.top:3006/api/getbooks',
     // URL 中的查询参数
     params: {
       id: 1
     }
   }).then(function (result) {
     console.log(result)
   })
   ```

2. 发起 POST 请求：
   
   ```js
   document.querySelector('#btnPost').addEventListener('click', async function () {
     // 如果调用某个方法的返回值是 Promise 实例，则前面可以添加 await！
     // await 只能用在被 async “修饰”的方法中
     const { data: res } = await axios({
       method: 'POST', 
       url: 'http://www.liulongbin.top:3006/api/post',
       data: {
         name: 'zs',
         age: 20
       }
     })
   
     console.log(res)
   })
   ```

3. 调用某个方法的返回值是pormise示例,则前面可以添加await
   
   1. 只能用在async修饰的方法中

#### vue-cli

1. 单页面应用程序:简称 SPA，顾名思义，指的是一个 Web 网站中只有唯一的一个 HTML 页面，所有的功能与交互都在这唯一的一个页面内完成。
2. vue-cli 是 Vue.js 开发的标准工具。它简化了程序员基于 webpack 创建工程化的 Vue 项目的过程。
3. 创建项目
   1. 快速创建Vue的项目:```vue create 项目的名称```
   2. 配置完成后使用```npm run serve```运行
4. src目录
   1. assets 文件夹：存放项目中用到的静态资源文件，例如：css 样式表、图片资源
   2. components 文件夹：程序员封装的、可复用的组件，都要放到 components 目录下
   3. main.js 是项目的入口文件。整个项目的运行，要先执行 main.js
   4. App.vue 是项目的根组件。
5. 在工程化的项目中，vue 要做的事情很单纯：通过 main.js 把 App.vue 渲染到 index.html 的指定区域中。
   1. App.vue 用来编写待渲染的模板结构
   2. index.html 中需要预留一个 el 区域
   3. main.js 把 App.vue 渲染到了 index.html 所预留的区域中
   4. Vue 实例的 ```$mount(选择器)``` 方法，作用和 el 属性完全一样！手动指令需要渲染的位置

#### vue组件

1. 组件化开发指的是：根据封装的思想，把页面上可重用的 UI 结构封装为组件，从而方便项目的开发和维护。

2. 每个 .vue 组件都由 3 部分构成，分别是：
   * template -> 组件的模板结构
   * script -> 组件的 JavaScript 行为
   * style -> 组件的样式(美化自己的结构)

3. script
   1. ![image-20220310181727626](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220310181727626.png)
   2. 组件中的data不能指向对象,组件中的data应该是个函数,return一个数据对象

4. less语法
   1. 组件的模板结构中应该包含一个根元素(例如:div)
   2. 在style标签上添加```lang=“less”```启用less语法

5. 组件的父子关系

   1. ![image-20220310205823177](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220310205823177.png)

   2. 使用组件时才会产生父子关系

   3. 使用步骤

      1. 使用 import 语法导入需要的组件(@代表当前目录)

      2. 使用 components 节点注册组件

      3. 以标签形式使用刚才注册的组件

         ![image-20220310210213024](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220310210213024.png)

      4. 通过components注册的是私有子组件

   4. 注册全局组件

      1. 在 vue 项目的 main.js 入口文件中，通过 Vue.component() 方法，可以注册全局组件。示例代码如下
      2. ![image-20220310211305434](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220310211305434.png)

   5. 组件的prop

      1. 某个方法只有一个非常简单的代码,可以不写method直接写成

         ```vue
         <button @click="count += 1">+1</button>
         ```

      2. 希望使用count的两个组件的初始值不同.使用组件的props,提高复用性.

         ![image-20220310212427333](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220310212427333.png)

         ![image-20220310212624954](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220310212624954.png)

         ![image-20220310212640466](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220310212640466.png)

      3. ==props的属性是只读的==

      4. 默认值default默认值:如果外界没有传默认值的时候生效

         ![image-20220310213837605](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220310213837605.png)

      5. props的type属性:可以通过 type 来定义属性的值类型

         ![image-20220310214153946](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220310214153946.png)

      6. props的rquired必选项:可以通过 required 选项，将属性设置为必填项，强制用户必须传递属性的值。

         ![image-20220310214238647](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220310214238647.png)

         

   6. 组件的样式冲突

      1. 默认情况下，写在 .vue 组件中的样式会全局生效，因此很容易造成多个组件之间的样式冲突问题。

      2. 原因:

         1. 单页面应用程序中，所有组件的 DOM 结构，都是基于唯一的 index.html 页面进行呈现的
         2. 每个组件中的样式，都会影响整个 index.html 页面中的 DOM 元素

      3. 解决:为每一个组件分配一个自定义属性,使用属性来控制样式的控制域

         ![image-20220310215422647](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220310215422647.png)

      4. 使用scoped属性来避免冲突
   
         ![image-20220310215609861](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220310215609861.png)
   
         5. /deep/样式穿透:如果给当前组件的 style 节点添加了 scoped 属性，则当前组件的样式对其子组件是不生效的。如果想让某些样式对子组件生效，可以使用 /deep/ 深度选择器
   
            1. 加了后改为```[].h5```,不加为```h5[]```
            2. 使用第三方组件库的时候,如果有修改组件默认样式的需求,需要用到deep
   
            
   
   
   
   
   
   
   
   ## 生命周期&数据共享
   
   ### 组件的生命周期
   
   #### 基本概念
   
   1. 生命周期（Life Cycle）是指一个组件从创建 -> 运行 -> 销毁的整个阶段，强调的是一个时间段。
   2. 生命周期函数：是由 vue 框架提供的内置函数，会伴随着组件的生命周期，自动按次序执行。
   
   3. ![image-20220311144150254](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220311144150254.png)
   
   
#### 组件创建时

1. beforecreated中组件:props/data/methods都处于不可用状态
2. ==created中组件都已创建好,但模板没有被创建==
   1. 在此阶段发起Ajax请求

3. beforeMount:把内存编译好的HTML结构渲染到浏览器中,当前还没有DOM结构,不能操作DOM结构
4. ==Mounted:已经包含了DOM元素==



#### 组件运行阶段

1. updated:修改数据时触发



### 组件之间的数据共享

1. 常见的两种关系:父子关系和兄弟关系

#### 父子关系数据共享

1. 父->子:自定义属性

   ![image-20220311151416762](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220311151416762.png)

   

   1. 不要修改porps的数据(即在子组件写自定义属性的数据)

2. 子->父:自定义事件

   1. 父组件定义数据项
   2. 在子组件使用this.$emit传送数据
   3. 父组件触发事件触发getNewCount处理函数
   4. 父组件通过形参得到子组件的值
   5. ![image-20220311153252132](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220311153252132.png)

#### 兄弟组件的数据共享

1.  vue2.x 中，兄弟组件之间数据共享的方案是 EventBus
2. ![image-20220311154310687](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220311154310687.png)
3. EventBus 的使用步骤 
   1. 创建 eventBus.js 模块，并向外共享一个 Vue 的实例对象
   2. 在数据发送方，调用 bus.\$emit('事件名称', 要发送的数据) 方法触发自定义事件 
   3. 在数据接收方，调用 bus.$on('事件名称', 事件处理函数) 方法注册一个自定义事件





### ref引用

1. 在不依赖于 jQuery 的情况下，获取 DOM 元素或组件的引用

2. 每个 vue 的组件实例上，都包含一个 \$refs 对象，里面存储着对应的 DOM 元素或组件的引用。默认情况下， 组件的 \$refs 指向一个空对象。

   ![image-20220311155944006](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220311155944006.png)

   

3. ref引用组件

   ![image-20220311163440168](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220311163440168.png)

4. 控制文本框和按钮的按需切换

   ![image-20220311164420075](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220311164420075.png)

5. 自动获得焦点
   1. ![image-20220311164550251](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220311164550251.png)
   2. 会出现undefined的错误,前面的成员没有定义
   3. 执行上一行代码时,文本框的展示需要一定的时间,所以下一行代码拿不到对象.
6. this.$nextTick(cb) 方法
   1. 组件的$nextTick(cb) 方法，会把cb 回调推迟到下一个DOM 更新周期之后执行。
   2. 通俗的理解是：等组件的DOM 更新完成之后，再执行cb 回调函数。从而能保证cb 回调函数可以操作到最新的DOM 元素。
   3. ![image-20220311165322095](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220311165322095.png)

7. 为什么不能使用update:当鼠标离开文本框时,数据更新,会再次触发update,文本框会获得焦点,可此时文本框已经隐藏

8. 数组的some方法

   1. foreach一旦开始会循环到结尾,无法再中间停止
   2. 寻找数组的指定项,使用```arr.some((item,index))```

9. 数组的every方法:判断数组的每一项是否满足某个条件.

10. 数组的reduce方法:

    1. 累加器,把每一次循环的结果加在一起

    2. 语法

       ```js
       const result=arr.filter(item=>item.state).reduce(累加的结果,累加项)=>{
       	return amt+=item.price*item.count
       },初始值)
       ```

    3. 简化写法```arr.filter(item=>item.state).reduce(累加的结果,累加项)=>return amt+=item.price*item.count,初始值)```





### 购物车案例

1. 使用axios发起请求
   1. 命令:```npm i axios -s```
   2. 在method中,定义initCartList函数请求数据,并使用async封装
   3. 在created中,调用封装的函数
   4. 只要是需要用到的数据,就要存到data中
2.  



