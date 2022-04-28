# html+css 回顾

## day1-标签使用

1. 图片标签
   1. <img src="" alt="" title=""></img>
   2. title:鼠标悬停的效果
   3. width 和 height:调整宽度和高度
2. 音频标签
   1. <audio src="" controls autoplay></audio>bt
   2. controls:显示播放的空间
   3. autoplay:自动播放
   4. loop:循环
3. 视频标签
   1. <video src=""></video>
   2. controls:显示播放的空间
   3. autoplay:自动播放
   4. loop:循环
4. 超链接
   1. <a herf=""></a>
   2. target 属性:
      1. \_self:覆盖原网页
      2. \_blank:保留原网页
   3. 空链接
      1. <a herf="#"></a>
      2. 跳转到网页顶部

## day2

### 列表

1. 无序列表(ul)
   1. ul:只能包裹 li 标签
   2. li 可以包裹任意内容
2. 有序列表(ol)
   1. ol:只能包裹 li 标签
   2. li 可以包裹任意内容
3. 自定义列表(dl)
   1. dt:自定义列表的标题
   2. dd:表项(默认缩进)

### 表格

1. tr:表示每行
2. td:表示每个单元格
3. border:边框宽度
4. caption:表格大标题
5. th:表格第一行的属性值

6. 合并单元格

   1. 明确单元格数量
   2. 左上原则,确定保留谁
   3. 给保留的单元格设置`<td rowspan="2">`或者 colspan

7. 表格的结构标签
   1. thead:头部
   2. tbody:主题
   3. tfoot:底部
   4. 标签包裹在 tr 的外面

### 表单

1. 文本框(text 和 password)

   1. ==placeholder:文本框提示信息==
2. 单选框(radio)

   1. name:分组
   2. checked:默认选中
3. 文件(file)

   1. multiple:多文件选择
4. 按钮(button)

   1. submit:提交
   2. reset:重置(需要 form 标签配合使用)
   3. button:无功能
   4. value:修改按钮的值
5. button 标签按钮<button>
6. 下拉菜单(select)

   1. option:每一项
   2. selected:默认选中
7. 文本域(textarea)

   1. cols:宽度
   2. rows:行数
8. label 标签
   1. 将文字和表单标签联系起来
   2. ![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-22-16-19-43.png)
   3. ![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-22-16-20-37.png)

### 语义化标签

1. div:分割网页,独占一行
2. span:在一行显示
3. 有语义的标签
   1. ![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-22-16-23-29.png)
4. 字符实体
   1. ![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-22-16-43-04.png)

## day3-css

### 选择器

1. 格式:选择器{css 属性名:属性值}
2. 标签选择器
   1. 通过 p 等标签名设定所有标签的样式
3. 类选择器

   1. 定义:通过 class=""
   2. 在 style 中,使用 `.class`设定样式
   3. 可以选中多个类
   4. 一个标签可以有多个类名,使用空格隔开

4. id 选择器

   1. 定义:#id 属性值
   2. id 属性值不可重复
   3. id 负责行为,class 负责样式
   4. id 选择器的权重更高

5. 通配符选择器
   1. 定义 \*{}
   2. 清楚默认样式

### 文字样式

1. font-weight

   1. 使用 100-900 的整百数来控制粗细

2. font-style

   1. italic:文字倾斜

3. 字体

   1. 无衬线字体:文字粗细均匀(黑体等)
   2. 衬线字体:文字粗细不均,有笔锋(宋体等)
   3. 等宽字体:每个文字/字母的宽度相等(consolas)
   4. 设定:font-family:微软雅黑,黑体,san-serif

4. 样式层叠问题

   1. 后边覆盖前面

5. font 复合写法
   1. font:style weight size family

### 文本样式

1. 文本缩进

   1. text-indent:
   2. em:1em=1 个文字的大小

2. 文本水平

   1. text-align=left/center/right
   2. 可以让文本/span/a/input/img 居中

3. 文本修饰

   1. ![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-22-17-54-43.png)
   2. 使用 none 清除超链接的下划线

4. 行高
   1. ![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-22-17-58-12.png)
   2. 文字间距=上间距+文本高度+下间距
5. 颜色
   1. 关键词:red blue
   2. 十六进制:#000000
   3. rgba 表示法

### 居中

1. 标签居中:
   1. margin:0 auto

### 选择器进阶

1. 后代选择器
   1. 语法:选择器 1 选择器 2{css}
   2. 找到选择器 1 所找标签的后代
2. 子代选择器
   1. 语法:选择器 1>选择器 2
   2. 只会选中儿子,孙子不能选中
3. 并集选择器
   1. 语法:选择器 1,选择器 2
   2. 选中多个标签
4. 交集选择器
   1. 语法:选择器 1.选择器 2
5. hover 伪类选择器
   1. 语法: 选择器:hover{css}
6. emmet 语法
   1. 简写,快速生成代码
   2. ![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-22-19-33-41.png)

### 背景相关属性

1. 背景颜色
   1. background-color(bgc)
   2. 默认透明:transparent
2. 背景图片
   1. background-imag:url(bgi)
   2. 盒子过大时会自动复制
3. 背景平铺
   1. background-repeat(bgr)
   2. ![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-22-19-39-38.png)
4. 背景位置
   1. background-position:center center(bg)
5. 连写
   1. background:color image repeat position
   2. 不分先后顺序
6. 背景图和 img 的区别
   1. img 需要设置 div 的宽和高,bgi 不用
   2. img 实现重要的图片

### 元素显示模式

1. 块级元素

   1. 独占一行
   2. 宽度默认父元素,高度由内容撑开
   3. 可以设置宽高

2. 行内元素
   1. 一行可以显示多个,不换行
   2. 不可以设置宽高,由内容决定

3. 行内块元素
   1. 一行可以显示多个
   2. 可以设置多个
   3. 代表标签:input,textarea,img

4. 显示模式转换
   1. ![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-22-20-10-03.png)

5. 元素嵌套注意点
   1. p不要套div,p,h等
   2. a可以嵌套任意元素,除了a元素


### css特性
1. 继承性
   1. 子元素有默认继承父元素的特性
   2. 文字类属性都能继承
   3. a标签的color会继承失效
   4. h标签的font-size失效

2. 层叠性
   1. 后边的会层叠前边的
   2. 选择器优先级相同的时候,才能通过层叠性判断结果

3. 优先级
   1. 不同选择器有不同的优先级
   2. 优先级:![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-23-10-05-46.png)
   3. important不能提升继承的优先级
   4. 权重叠加:(行内样式,id选择器,类选择器,标签选择器)
      1. 数字相同比较层叠性
      2. 如果都是继承,比较父级,谁的父级高,继承谁
4. css上一行代码出错,下一行会受影响


### 盒子模型
1. 边框
   1. 设置边框的粗细
   2. ![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-23-10-45-05.png)
   3. 设置某个方向的线,使用border-方向(例如:border-top)
2. 盒子尺寸
   1. 盒子宽度=边框+内容宽度(设置的盒子宽度)
   2. 盒子高度=边框+内容高度(设置的盒子高度)
   3. 盒子被撑大时,手动减去宽高
3. 内边距
   1. 也会撑大盒子
   2. 设置某个方向的内边距,使用padding-方向(例如:padding-top)
   3. 盒子宽高=边框+内边距+内容宽高(设定的width和height)
4. 新浪例子优化
   1. 设定padding实现内容自动撑开
5. 自动内减
   1. css3实现
   2. 设定属性box-sizing:border-box
   3. 加了border和padding,不需要手动减法
6. 外边距
   1. 设定方法与padding一摸一样
7. 清楚默认内外边距
   1. 标签都有默认的边距(a,body,p等)
   ```css
   *{
      margin:0
      padding:0
   }
   ```
8. 版心居中
   1. 版心:网页的有效内容
   ```css
   margin: 0 auto
   ```
9. 去掉列表的符号
   ```css
   ul{
      list-style:none;
   }
   ```
10. 从外到内,先宽高背景色,放内容,调节位置,控制文字细节

11. margin合并
    1.  垂直布局的块级元素,上下的margin会合并
    2.  结果:取两者margin的最大值
    3.  只给一个盒子设置margin即可

12. margin塌陷
    1.  互相嵌套的块级元素,子元素的margin-top会作用在父级上
    2.  解决办法:![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-23-13-16-16.png)

13. 行内标签的垂直方向的margin和padding无效
    1.  使用line-height改变垂直方向的位置


### 结构伪类选择器
1. 利用标签的关系查找元素
2. nth的公式:![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-23-13-26-45.png)

### 伪元素
1. 使用css模拟出的标签效果
   1. 一般用于装饰用的小图
2. 使用方法:![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-23-13-36-02.png)
3. 必须设置content属性
4. 伪元素默认时行内元素

### 浮动
1. 标准流:默认的排版规则,又称文档流

2. 行内块的问题:代码换行时会产生默认一个空格的间距
   1. 使用浮动去解决
3. 浮动的标签会脱离标准流的控制,不占用标准流的位置
4. 浮动可以设置宽高,在一行排列
   1. 具备行内块的特点
5. 不能使用text-align:center/margin:0 auto
   1. 使用一个版心div来完成居中
6. css书写顺序
   1. 浮动或者display
   2. 盒子模型相关的属性(margin padding border width等)
   3. 文字样式
7. 父级的宽度不够,子级会自动换行
8. 清除浮动
   1. 目的:清除浮动给其他标签带来的影响
   2. 原因:父元素没有高度,子元素浮动脱标准流,不占位置
   3. 解决方法:需要父元素有高度
9. 清除浮动的其他方法
   1. 额外标签法
      1. 在父元素的最后添加一个块级标签
      2. 给块级元素设置: clear:both
      3. 缺点:影响结构
   2. 单伪元素清楚法
      1. 在项目中使用
      ```css
      .clearfix::after{
         content:"";
         display:block;
         clear:both;
      }
      ```
   3. 双伪元素清除法
      1. ![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-23-14-14-36.png)
      2. 真正清除浮动的标签
         1. before:解决外边距塌陷
   4. 给父元素设置: overflow:hidden



### 定位
1. 实现两个标签叠在一起,盒子叠在一起的情况
   1. 也可以实现盒子固定在某个位置
2. 设置属性:position
   1. 属性值:![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-23-15-57-23.png)
3. 相对定位:relative
   1. 相对于之前的位置移动
   2. 特点:![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-23-16-00-09.png)
   3. 要配合方位属性移动(left和top)
4. 绝对定位:absolute
   1. 先找已经定位的父级,如果有这样的父级,以这个父级为参考
   2. 如果没有,以浏览器窗口为准
   3. 脱离标准流
   4. 不具备原有的块标签的特点,具备行内块特点.(如果没有宽度也没有内容,盒子的宽度尺寸为0)
5. 子绝父相
   1. 让子元素相对于父元素自由移动
6. 居中
   1. 绝对定位的盒子不能使用margin:0 auto
   2. 使用left:50%和margin:50%*盒子宽度*-1 实现居中
   3. 使用transform:translate(-50%,-50%)来实现居中
7. 固定定位:fixed
   1. 脱标
   2. 盒子的位置固定不变
   3. 具备行内块的特点(如果没有宽度也没有内容,盒子的宽度尺寸为0)
8. 元素的层级关系
   1. 层级关系:标准流<浮动<定位
   2. 定位的盒子,后边的标签在最上边
   3. 修改定位元素的层级:z-index
      1. 数字越大,层级越高
      2. 默认为0
      3. 需要配合定位才能有效
   

### 装饰
1. 基线:文字排版根据基线对齐
   1. 浏览器遇到行内和行内块标签时,默认按基线对齐
2. 垂直对齐:vertical-align
   1. 属性值:![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-23-16-45-44.png)
   2. 找到大的使用这个属性值
   3. 场景:
      1. 文本框和表单按钮无法对齐问题
      2. input和img无法对齐问题
      3. div中的文本框，文本框无法贴顶问题
      4. div不设高度由img标签撑开，此时img标签下面会存在额外间隙问题
      5. 使用line-height让img标签垂直居中问题(父lh子v:middle)
         1. 使用text-align实现盒内居中
3. 光标类型(cursor)
   1. 属性值:![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-23-16-54-34.png)
4. 边框圆角(border-radius)
   1. 原理:![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-23-16-56-21.png)
   2. 正圆:
      1. 盒子是正方形
      2. border-radius:50%
   3. 胶囊:
      1. 盒子是长方形
      2. border-radius:盒子高度的*50%
5. 溢出显示效果(overflow)
   1. 属性值:![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-23-16-59-48.png)
6. 元素本身隐藏(visibility和display)
   1. 区别:![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-23-17-02-12.png)
7. opacity:会使整体一起透明