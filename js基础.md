# JavaScript

## 基础

1. 当有多个表达式时,左边的表达式可以确定结果时,不在继续运算右边表达式的值
   1. 表达式 1&表达式 2
   2. 如果 1 为真,返回表达式 2
   3. 如果 1 为假,返回表达式 1
2. 实参与形参的个数:

   1. 实参>形参:只取到形参的个数
   2. 实参<形参:剩余的形参用 undefined

3. return 只能返回一个值,以最后一个为准.如果要返回多个值,使用数组.
4. 如果函数没有 return,返回 undefined.

5. 匿名函数

   1. var fun=function(){}
   2. fun 是变量名,不是函数名

6. js 引擎执行分为两步:

   1. 预解析:js 引擎会把所有的 var 和 function 提到当前作用域的最前面(只提升 var)
   2. 执行:

7. 一个变量如果没有声明,直接赋值,视作 全局变量

## 对象

1. 字面量:

   ```javascript
   var obj={
   uname="",
   age:"",
   sayhi:function(){}
   }
   ```

   1. 调用属性:obj['age']

2. new object():

   ```JavaScript
   var obj=new object() obj.uname=
   ```

3. 构造函数

   ```JavaScript
   function star(uname,age,sex){
   this.name=uname;
   this.age=age;
   this.sex=sex;
   this.sing=funciton(sang){
      console.log(sang)
      }
   }
   var ldh=new star("ldh",18,"male"); //调用函数
   ```

4. new 的执行过程

   1. 在内存创建一个空对象
   2. this 指向该对象
   3. 执行构造函数的代码
   4. 返回对象

5. 遍历对象
   ```JavaScript
   for (var k in obj){
      console.log(obj[k])
   }
   ```
   1. k是属性名(键)
   2. obj[k]是值

## 内置对象

1. 分为三类:自定义对象,内置对象,浏览器对象(js 独有)
   1. 前两者是 js 基础 属于 ECMAScript
2. Math.round: -.5 向大的方向取(console.log(Math.round(-1.5)) //-1)

### Date

1. 没有参数:当前时间
2. 参数型:数字型和字符串型(重要)

3. ![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-22-12-49-36.png)

4. getmonth():返回的月份小 1.

5. gettime 和 valueof:现在时间距离 1970.1.1 的总毫秒数(时间戳)
   1. 简单写法:`var date=+new Date()`
   2. H5 新增:Date.now()

### Array

1. 创建数组

   1. 数组字面量:`var arr=[1,2,3]`
   2. new Array:`var arr=new Array(length)`
      1. `var arr=new Array(2,3)` //数组内存储了 2 和 3

2. 检测类型:`instanceof()`

   1. 检测是否为数组:`Array.isArray()`

3. 添加删除数组元素:

   1. ![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-22-13-11-25.png)

4. sort 方法可以使用 函数表达式 方便地书写：

```javascript
var numbers = [4, 2, 5, 1, 3];
numbers.sort(function(a, b) {
  return a - b;
});
console.log(numbers);

也可以写成：
var numbers = [4, 2, 5, 1, 3];
numbers.sort((a, b) => a - b);
console.log(numbers);

// [1, 2, 3, 4, 5]

```
5. indexof(要查找的元素,查找开始的位置)
   1. -1:表示从数组的最后一个元素开始查找

6. 数组转化为字符串
   1. toString()
   2. join(分隔符):可以设定分隔符


### 基本包装类型
1. 三种包装类型:String Number Boolean
2. 字符串的值不可变
3. 根据位置返回字符
   1. ![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-22-13-41-20.png)

4. 字符串的拼接
   1. ![](https://raw.githubusercontent.com/Furakafuka/ABC/main/2022-02-22-13-46-55.png)

5. 字符串的分割
   1. split:将字符串分割为数组