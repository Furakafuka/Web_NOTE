# js进阶

## day1

### 导读

1. web api:一套操作浏览器的api(bom和dom)
2. dom:文档对象模型
   1. 处理文档的接口,改变网页的结构,内容和样式
3. dom树
   1. ![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-23-19-18-48.png)
   2. 文档:一个页面
   3. 元素:所有的标签
   4. 节点:所有的内容都是节点(标签,属性,文本,注释等)
4. 获取元素
   1. 根据id获取
      1. api:document.getElementById('id');
      2. 将script写到标签的下面
      3. 返回的是一个元素对象
   2. 根据标签名获取
      1. api:element.getElementsByTagName("标签名");
      2. 得到的元素对象是动态的
      3. 返回的是伪数组
   3. 通过类名获取
      1. document.getElementsByClassName(‘类名’);// 根据类名返回元素对象集合
   4. 通过选择器
      1. document.querySelector('选择器'); // 根据指定选择器返回第一个元素对象
      2. document.querySelectorAll('选择器'); // 根据指定选择器返回
   5. 获取body和html
      1. doucumnet.body // 返回body元素对象
      2. document.documentElement // 返回html元素对象

### 事件基础

1. 事件三要素:事件源,事件类型,事件处理程序
   1. btn.onclick=funciton(){} //事件处理
2. 执行事件:获取事件源,注册事件,添加处理程序

### 操作元素

1. 改变元素内容:element.innerText/element.innerHTML
2. innerHTML和innerText
   1. innerText:不识别html标签,innerHtmL支持
   2. 可读写
   3. innerHtmL保留空格和换行
3. 常用属性
   1. innerText、innerHTML 改变元素内容
   2. src、href
   3. id、alt、title
4. 表单元素修改
   1. 常见属性:type、value、checked、selected、disabled
   2. disabled:禁用表单
5. 样式属性修改
   1. element.style 行内样式操作
   2. element.className 类名样式操作
   3. 例如:div.style.backgroundColor=""
   4. JS 修改 style 样式操作，产生的是行内样式，CSS 权重比较高
6. 遍历精灵图

```JavaScript
    var lis = document.querySelectorAll('li');
    for (var i = 0; i < lis.length; i++) {
    // 让索引号 乘以 44 就是每个li 的背景y坐标 index就是我们的y坐标
    var index = i * 44;
    lis[i].style.backgroundPosition = '0 -' + index + 'px';
    }
```

7. 通过className修改类名

   1. element.className="newclassName"
   2. 如果想要保留:使用多类名选择器
8. 总结

   1. ![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-23-20-33-42.png)
9. 排他思想

   1. 先取掉其他的背景颜色
   2. 再设定想要的按钮的背景颜色
10. 案例:全选按钮

    1. 思路:![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-23-20-50-21.png)
    2. this.cheked:获取选中状态
11. 获取自定义属性的值

    1. element.getAttribute("属性")
    2. 可以获取自定义属性的值
12. 设定自定义属性的值

    1. element.setAttribute(‘属性’)
13. H5自定义属性

    1. 有些数据不用保存到数据库
    2. H5规定自定义属性以 data-属性名 作为自定义属性名
    3. H5使用element.dataset.index获取属性值
    4. 如果自定义属性有多个 - ,获取属性名时要使用驼峰命名法
       1. 例如: data-list-name -> div.dataset.listName

### 节点操作

1. 逻辑性强,但是兼容性稍差
2. 节点概述:![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-23-21-32-00.png)
3. 节点至少拥有nodeType（节点类型）、nodeName（节点名称）nodeValue（节点值）这三个基本属性。

   1. 元素节点 nodeType 为 1
   2. 属性节点 nodeType 为 2
   3. 文本节点 nodeType 为 3 （文本节点包含文字、空格、换行等)
4. 常见的层级关系为:父子兄层级关系
5. 父节点

   1. 使用:node.parentNode
   2. 获得的是最近的父节点
6. 子节点

   1. parentNode.childNodes（标准）
   2. 会得到所有的子节点.包括元素节点，文本节点等。
   3. 使用nodeType获取想要的节点
   4. 使用parentNode.children（非标准）获取所有子元素节点
7. 第一个和最后一个

   1. parentNode.firstChild : 返回第一个子节点
   2. parentNode.lastChild  : 返回最后一个子节点
   3. parentNode.firstElementChild : 返回第一个子元素节点
   4. parentNode.lastElementChild :返回最后一个子元素节点
   5. 实际开发的写法

      1. parentNode.chilren[0]
      2. parentNode.chilren[parentNode.chilren.length - 1]
8. 兄弟节点

   1. 下一个兄弟元素节点:node.nextSibling
   2. 上一个兄弟元素节点:node.previousSibling
      1. 包括元素节点和文本节点
   3. 下一个兄弟元素节点:node.nextElementSibling
   4. 上一个兄弟元素节点:node.previousElementSibling
      1. 有兼容性问题
9. 创建节点

   1. document.createElement('tagName')
   2. 动态创建元素节点
   3. 添加节点(父亲添加孩子):
      1. node.appendChild(child)
      2. node.insertBefore(child, 指定元素)
      3. 在后面追加元素
10. 删除节点

    1. node.removeChild(child)
    2. 使用`<a href="javascript:">`阻止链接跳转
    3. 删除链接所在的父节点
11. 克隆节点

    1. node.cloneNode()
    2. 如果括号参数为空或者为 false ，则是浅拷贝，即只克隆复制节点本身，不克隆里面的子节点。
12. document.write 是直接将内容写入页面的内容流，但是文档流执行完毕，则它会导致页面全部重绘
13. innerHTML 创建多个元素效率更高（不要拼接字符串，采取数组形式拼接），结构稍微复杂

### DOM重点核心

1. 创建:![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-24-17-17-20.png)
2. 增:![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-24-17-19-01.png)
3. 删:![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-24-17-19-19.png)
4. 改:![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-24-17-19-32.png)
5. 查:![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-24-17-19-43.png)
6. 属性操作:![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-24-17-19-58.png)
7. 事件操作:![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-24-17-20-17.png)

## day2

### 注册事件

1. 给元素添加事件
2. 传统方式

   1. 利用 on 开头的事件 onclick
   2. <button onclick=“alert('hi~')”>`</button>`
   3. btn.onclick = function() {}
   4. 特点： 注册事件的唯一性
   5. 同一个元素同一个事件只能设置一个处理函数，==最
      后注册的处理函数将会覆盖前面注册的处理函数==
3. 方法监听

   1. addEventListener() 它是一个方法
   2. 同一个元素同一个事件可以注册多个监听器
4. addEventListener()

   1. ``eventTarget.addEventListener(type, listener, useCapture)``
   2. type：事件类型字符串，比如 click 、mouseover ，注意这里不要带on(带引号)
   3. listener：事件处理函数，事件发生时，会调用该监听函数
   4. useCapture：可选参数，是一个布尔值，默认是 false.
   5. ==同一个元素,同一个事件可以添加多个监听器(事件处理程序)==
   6. 不要使用匿名函数

### 删除事件

1. 传统方式
   1. ``eventTarget.onclick = null;``
2. 方法监听注册方式
   1. ``eventTarget.removeEventListener(type, listener, useCapture);``
   2. ``eventTarget.detachEvent(eventNameWithOn, callback);``

### DOM事件流

1. 事件流描述的是从页面中接收事件的顺序。事件发生时会在元素节点之间按照特定的顺序传播，这个传播过程即 DOM 事件流。
2. DOM事件流阶段

   ![image-20220227103151274](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220227103151274.png)

![image-20220227103304484](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220227103305285.png)

3. ``addEventListener(type, listener[, useCapture])``第三个参数如果是 true，表示在事件捕获阶段调用事件处理程序；如果是 false（不写默认就是false），表示在事件冒泡阶段调用事件处理程序。(视频P18)

### 事件对象

1. 在监听函数小括号内,当作形参

   1. ``eventTarget.onclick = function(event) {}``
   2. 可以自己命名(eve,e等)
   3. 有兼容性问题,ie678通过window.event获取对象
2. 事件对象常用的属性和方法

   ![image-20220227104556145](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220227104556145.png)

   1. 返回触发事件对象:注册的是ul,点击的是li
   2. 阻止默认行为(让链接不跳转,让按钮不提交)
      1. return fasle也能阻止默认行为

### 阻止冒泡

1. 标准写法:``e.stopPropagation()``
2. 非标准:``e.cancelBubble = true;``
3. 事件委托:
   1. 传统:使用循环给所有的li注册事件
   2. ==不是每个子节点单独设置事件监听器，而是事件监听器设置在其父节点上，然后利用冒泡原理影响设置每个子节点==
      1. 以上案例：给 ul 注册点击事件，然后利用事件对象的 target 来找到当前点击的 li，因为点击 li，事件会冒泡到 ul 上，ul 有注册事件，就会触发事件监听器。(p67)

### 常用键鼠事件

1. 常用鼠标事件

   ![image-20220227110424124](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220227110424124.png)

   ![image-20220227110812000](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220227110812000.png)

   1. 前两个获得的鼠标坐标与是否拖动右边无关
2. 常用键盘事件

   ![image-20220227110703838](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220227110703838.png)

   ![image-20220227111932922](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220227111932922.png)

   1. keydown和keypress的特点:事件触发时,文字还没有落入文本框中
   2. keyup触发时,文字已经落入文本框

## day3

### BOM

1. BOM:浏览器对象模型,它提供了独立于内容而与浏览器窗口进行交互的对象，其核心
   对象是 window.缺乏标准
2. 与DOM的区别

   ![image-20220227114240255](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220227114240255.png)
3. BOM构成

   ![image-20220227114440358](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220227114440358.png)

   1. 它是 JS 访问浏览器窗口的一个接口。
   2. 它是一个全局对象。定义在全局作用域中的变量、函数都会变成 window 对象的属性和方法
   3. window下的一个特殊属性 window.name

### BOM常见事件

1. 加载事件

   1. ``window.onload = function(){}``
   2. 如果有多个，会以最后一个 window.onload 为准
   3. ``window.addEventListener("load",function(){});``这种方法无限制
   3. load在页面元素全部加载完毕
   3. DOMContentLoaded在DOM加载完毕,不包括图片,css,flash等,比load更快

2. 调整窗口大小

   1. ```JavaScript
      window.onresize = function(){}
      window.addEventListener("resize",function(){})
      ```

   2. 窗口大小像素变化,触发
   3. 我们经常利用这个事件完成响应式布局.window.innerWidth 当前屏幕的宽度

3. 定时器

   1. setTimeout(调用函数,延迟毫秒数)
      1. 这个调用函数可以直接写函数，或者写函数名或者采取字符串‘函数名()'三种形式。第三种不推荐
      2. 因为定时器可能有很多，所以我们经常给定时器赋值一个标识符。
      3. ==调用一次就结束==
   2. ==回调函数:上一件事干完,才去调用这个函数==
   3. 清除定时器:```window.clearTimeout(timeoutID)```
   4. setInterval(回调函数, 间隔的毫秒数)
      1. setInterval() 方法重复调用一个函数,==开启期间重复调用一个函数==
   5. 清除定时器:```window.clearInterval(intervalID);```
      1. 定时器最好设置一个全局变量

4.  this的指向问题

   1. 一般情况下this的最终指向的是那个调用它的对象
   2. 全局作用域或者普通函数中this指向全局对象window
   3. ==注意定时器里面的this指向window==
   4. 方法调用中谁调用this指向谁
   5. 构造函数中this指向构造函数的实例(p87)





### JS执行机制

1. JS是单线程的
2. 同步:前一个任务结束后再执行后一个任务，程序的执行顺序与任务的排列顺序是一致的、同步的
3. 异步:你在做一件事情时，因为这件事情会花费很长时间，在做这件事的同时，你还可以去处理其他事情。
4. ==同步任务:同步任务都在主线程上执行，形成一个执行栈。==
5. ==异步任务:JS 的异步是通过回调函数实现的。,在任务队列中==
6. 执行机制:![image-20220227160833481](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220227160833481.png)



### Location对象

1. 用于获取或设置窗体的 URL，并且可以用于解析 URL 

2. URL组成:

   1. ```
      protocol://host[:port]/path/[?query]#fragment
      http://www.itcast.cn/index.html?name=andy&age=18#link
      ```

   2. ![image-20220227161611053](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220227161611053.png)

3. 属性:![image-20220227161248112](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220227161248112.png)

4. Location方法

   ![image-20220227162750400](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220227162750400.png)





### navigator对象

1. navigator 对象包含有关浏览器的信息，它有很多属性，我们最常用的是userAgent，该属性可以返回由客户机发送服务器的 user-agent 头部的值
2. userAgent中包括用户的登陆设备信息



### history对象

1. 与浏览器历史记录进行交互
2. history对象方法:![image-20220227163346827](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220227163346827.png)





## day4

### PC端网页特效

1. offset:可以动态的得到该元素的位置（偏移）、大小等

   1. 常用属性:

      ![image-20220227163717922](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220227163717922.png)

   2. 如果没有父亲,以body为准

2. 与style的区别

   ![image-20220227164249235](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220227164249235.png)

3. client:可以动态的得到该元素的边框大小、元素大小等,获取元素可视区的相关信息.

   1. 常用属性:

      ![image-20220227165827096](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220227165827096.png)

   2. 与offset的区别:不包括边框

4. 立即执行函数:不需要调用,立即执行的函数

   1. 写法:```(function() {})()``` 或者``` (function(){}())```
   2. 第二个小括号可以看作调用函数(实参),传给第一个括号的形参
   3. ==创建一个独立的作用域。 避免了命名冲突问题==



### flexibleJS源码

1. 将window和document传给函数,函数内可以使用这两个参数
2. dpr:物理像素比
3. setbodyfontsize:设置body的大小
   1. 使用domcontentloaded等待加载完毕
4. setremunit:设置html元素的文字大小,将屏幕十等分
5. 当页面尺寸变化时,重新设置rem的大小
6. 触发load事件
   1. a标签的超链接
   2. F5或者刷新按钮（强制刷新）
   3. 前进后退按钮





### scroll系列

1. 使用 scroll 系列的相关属性可以动态的得到该元素的大小、滚动距离等。

2. 常用属性:

   ![image-20220227172309465](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220227172309465.png)

3. 获得的是内容的实际大小,哪怕内容超出盒子

4. 属性:

   ![image-20220227172900304](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220227172900304.png)

   5. 页面被卷去的头部：可以通过window.pageYOffset 获得

      1. 注意，==元素被卷去的头部是 element.scrollTop , 如果是页面被卷去的头部 则是 window.pageYOffset==

   6. 三大系列总结

      ![image-20220227173812951](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220227173812951.png)

   7. mouseover 鼠标经过自身盒子会触发，经过子盒子还会触发。 ==mouseenter 只会经过自身盒子触发==





### 动画函数

1. 基本移动动画
   1. 使用定时器重复条件
   2. 停止动画本质是停止定时器
   3. 需要添加定位,才能使用element.style.left
2. 简单动画函数封装
   1. obj:目标对象,target:目标位置
   2. 添加不同元素的定时器:使用obj.timer来指定定时器
   3. 开启太多定时器,速度会加快,只能有一个定时器,需要清除原本的定时器,保留当前的定时器
3. 缓动动画
   1. 元素的运动速度有变化,不匀速
   2. 核心算法：(目标值 - 现在的位置 ) / 10 做为每次移动的距离 步长
   3. ==步长值需要取整==
   4. 在多个目标值移动:```step>0?ceil:floor```(如果是正值，则步长 往大了取整如果是负值，则步长 向小了取整)
4. 添加回调函数
   1. 在定时器结束的位置写回调函数
5. 节流阀
   1. 连续点击会有播放过快的问题
   2. 开始设置一个标志为true,当flag=true时,设置变量为false,然后再执行函数.然后利用回调函数打开水龙头.
6. 返回顶部
   1. 滚动窗口至文档中的特定位置。window.scroll(x, y)(注意，里面的x和y 不跟单位，直接写数字)





### 移动端网页特效

1. 触屏事件

   ![image-20220227210652171](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220227210652171.png)

2. 触摸事件对象
   1. ![image-20220227210949653](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220227210949653.png)
3. 拖动元素
   1. 触摸元素 touchstart： 获取手指初始坐标，同时获得盒子原来的位置
   2. 移动手指 touchmove： 计算手指的滑动距离，并且移动盒子
   3. 离开手指 touchend
   4. ==手指移动也会触发滚动屏幕所以这里要阻止默认的屏幕滚动 e.preventDefault();==



### 本地存储

1. 特性

   1. 数据存储在用户浏览器中
   2. 设置、读取方便、甚至页面刷新不丢失数据
   3. 容量较大，sessionStorage约5M、localStorage约20M
   4. 只能存储字符串，可以将对象JSON.stringify() 编码后存储

2. window.sessionStorage

   1. 生命周期为关闭浏览器窗口
   2. 在同一个窗口(页面)下数据可以共享
   3. 以键值对的形式存储使用
   4. ![image-20220227213439897](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220227213439897.png)

3. window.localStorage

   1. 声明周期永久生效，除非手动删除 否则关闭页面也会存在

   2. 可以多窗口（页面）共享（同一浏览器可以共享）

   3. ![image-20220227214123820](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220227214123820.png)

      
