



# jQuery

## day1

### 顶级对象

1. $是jQuery的别称(可以替换为jQuery)
2. $是jQuery的顶级对象,相当于原生JS的window



### jQuery 对象和 DOM 对象

1. 用原生 JS 获取来的对象就是 DOM 对象 
2. jQuery 方法获取的元素就是 jQuery 对象.==本质是$对DOM元素进行了包装==
3. 只有 jQuery 对象才能使用 jQuery 方法，DOM 对象则使用原生的 JavaScirpt 方法。
4. 相互转换:
   1. DOM->jQuery:$(DOM对象)
   2. jQuery->DOM:$('div') [index] index 是索引号



## day2

### 常用API

1. 基础选择器:```$(“选择器”)// 里面选择器直接写 CSS 选择器即可，但是要加引号```

   ![image-20220228100100687](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220228100100687.png)

2. 层级选择器:

   ![image-20220228100156799](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220228100156799.png)

3. $不能使用style修改样式

   1. $样式设置:```$('div').css('属性', '值')```
   2. 可以修改所有的div的颜色==隐式迭代==

4. 隐式迭代:将所有匹配元素进行内部遍历,给每一一个元素设置css

5. 筛选选择器

   ![image-20220228101735851](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220228101735851.png)

6. 筛选方法:

   ![image-20220228102020930](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220228102020930.png)

7. 排他思想:

   ```javascript
   $(this).css(“color”,”red”);
   $(this).siblings(). css(“color”,””);
   ```



###  jQuery 样式操作

1. 参数只写属性名，则是返回属性值

2. 参数是属性名，属性值，逗号分隔，是设置一组样式，==属性必须加引号==，值如果是数字可以不用跟单位和引号

3. 参数可以是对象形式，方便设置多组样式。

   ```javascript
   $(this).css({ "color":"white","font-size":"20px"});
   ```

4. 设置类样式方法
   1. ![image-20220228104438456](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220228104438456.png)
   2. 切换类:点击一次可以添加类,再次点击可以移除类
   3. ==jQuery 里面类操作只是对指定类进行操作，不影响原先的类名。==

 



### jQuery 效果

1. 显示效果

   1. show([speed,[easing],[fn]])
   2. ![image-20220228105414081](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220228105414081.png)

2. 隐藏效果

   1. hide([speed,[easing],[fn]])
   2. ![image-20220228105414081](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220228105414081.png)

3.  切换语法规范

   1. toggle([speed,[easing],[fn]])
   2. ![image-20220228105414081](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220228105414081.png)

4. 下滑效果

   1. slideDown([speed,[easing],[fn]])
   2. ![image-20220228105414081](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220228105414081.png)

5. 上滑效果

   1. slideUp([speed,[easing],[fn]])
   2. ![image-20220228105414081](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220228105414081.png)

6.  滑动切换效果

   1. slideToggle([speed,[easing],[fn]])
   2. ![image-20220228105414081](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220228105414081.png)

7. ==事件切换==

   1. hover([over,]out)
   2. ![image-20220228110033380](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220228110033380.png)

8. 停止排队

   1. stop() ==写到动画或者效果的前面==， 相当于停止结束上一次的动画。

9. 淡入淡出效果:

   1. fadeOut([speed,[easing],[fn]])
   2. fadeIn([speed,[easing],[fn]])
   3. fadeToggle([speed,[easing],[fn]])
   4. fadeTo([[speed],opacity,[easing],[fn]])
      1. opacity 透明度必须写，取值 0~1 之间。

10. 自定义动画

    1. animate(params,[speed],[easing],[fn])

    2. ==params: 想要更改的样式属性，以对象形式传递，必须写。 属性名可以不用带引号， 如果是复合属性则需要采取驼峰命名法 borderLeft。==

    3. ```javascript
       $("div").animate({left: 500,top: 300,opacity: .4,width: 500}, 500); //最后一个500时动画时长
       ```





### jQuery 属性操作

1. 设置或获取元素固有属性值 prop()
   1. 所谓元素固有属性就是元素本身自带的属性
   2. 设置:```prop(''属性'', ''属性值'')```
2. 设置或获取元素自定义属性值 attr()
   1. 设置:```attr(''属性'', ''属性值'') // 类似原生 setAttribute()```
3. 数据缓存data()
   1. data() 方法可以在指定的元素上存取数据，并不会修改 DOM 元素结构。
   2. 一旦页面刷新，之前存放的数据都将被移除
   3. ```data(''name'',''value'') // 向被选元素附加数据```
   4. ```$("span").date(''name'')// 向被选元素获取数据```
4. 内容文本值
   1. ![image-20220228150359560](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220228150359560.png)
5. ==*parents(".p-num") 返回指定的祖先元素*==
6. ==tofixed(n) //保留n为小数==





### jQuery 元素操作

1. 遍历元素
   1. ```$("div").each(function (index, domEle) { xxx; }）```
      1.  ==所以要想使用jquery方法，需要给这个dom元素转换为jquery对象 $(domEle)==
      2. ==demEle 是每个DOM元素对象，不是jquery对象==
   2. ```$.each(object，function (index, element) { xxx; }）```
      1. $.each()方法可用于遍历任何对象。主要用于数据处理，比如数组，对象
      2. index 是每个元素的索引号; element 遍历内容
2. 添加元素
   1. 内部添加
      1. 添加到后面:element.append(''内容'')
      2. 添加到前面:element.prepend(''内容'')
   2. 外部添加
      1. 把内容放入目标元素后面:element.after(''内容'')
      2. 把内容放入目标元素前面:element.before(''内容'')
   3. ==内部添加元素，生成之后，它们是父子关系。外部添加元素，生成之后，他们是兄弟关系==
3. 删除元素
   1. ![image-20220228153824940](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220228153824940.png)





### jQuery 事件

1. 单个事件注册:

   1. ```$(“div”).click(function(){ 事件处理程序 })```
   2. ```element.事件(function(){})```

2. 事件处理:

   1. on绑定事件

      1. element.on(events,[selector],fn)

      2. 可以绑定多个事件

         ```javascript
         //如果事件处理程序相同
         $(“div”).on(“mouseover mouseout”, function() {
         $(this).toggleClass(“current”);
         });
         ```
      
         ```javascript
         $(“div”).on({
         mouseover: function(){},
         mouseout: function(){},
         click: function(){}
         });
         ```
      
      
      3. 可以事件委派操作
      
         ```javascript
         $('ul').on('click', 'li', function() {
         alert('hello world!');
         });
         ```
      
      4. on() 可以给动态生成的元素绑定事件(给后面创建的元素绑定事件)
      
         ```javascript
         $(“div").on("click",”p”, function(){
         alert("俺可以给动态生成的元素绑定事件")
         });
         ```

   2. 事件处理 off() 解绑事件

      1. ```JavaScript
         $("p").off() // 解绑p元素所有事件处理程序
         $("p").off( "click") // 解绑p元素上面的点击事件 后面的 foo 是侦听函数名
         $("ul").off("click", "li"); // 解绑事件委托
         ```

   3. 自动触发事件
      1. element.trigger("type") // 第二种自动触发模式
      2. element.triggerHandler(type) // 第三种自动触发模式

3. 事件对象

   1. element.on(events,[selector],function(event) {}
   2. event是事件对象





## day3 

### jQuery 对象拷贝

1. ```$.extend([deep], target, object1, [objectN])```
   1. ![image-20220228170550660](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220228170550660.png)
   2. 会覆盖掉原本的数据
2.  jQuery 多库共存
   1. jQuery使用$作为标示符，随着jQuery的流行,其他 js 库也会用这作为标识符， 这样一起使用会引起冲突。
   2. 解决:. 把里面的 $ 符号 统一改为 jQuery。 比如 jQuery(''div'')
   3. jQuery 变量规定新的名称：\$.noConflict() var xx = \$.noConflict();
      1. 之后就可以用xx来代替jQuery的$这个顶级对象了
3. 图片懒加载:只加载可视区域的图片,随用户滑动而显示



### jQuery尺寸操作

1. 尺寸

   ![image-20220302164837488](https://raw.githubusercontent.com/Furakafuka/ABC/main/image-20220302164837488.png)

   * 以上参数为空，则是获取相应值，返回的是数字型

2. 位置

   1. offset:
      1. 获取的是与==文档==的偏移,与父级无关
      2. 该方法有2个属性 left、top 。offset().top 用于获取距离文档顶部的距离，offset().left 用于获取距离文档左侧的距离。
      3. 可以设置元素的偏移：offset({ top: 10, left: 30 });
   2. position
      1. 获取的是与==带有定位的父级==的偏移坐标
      2. 该方法只能获取。
   3. scrollTop/scrollLeft
      1. scrollTop() 方法设置或返回被选元素==被卷去的头部==。
   4. 带有动画返回顶部
      1. 但是是元素做动画，因此 $(“body,html”).animate({scrollTop: 0})