---
title: 《JavaScript高级程序设计》笔记
date: 2016-08-17 10:47:38
tags:
- JavaScript
---
#### 1.数据类型
```JavaScript
var message;	//message = undefined

var message = 1;	//局部变量    
message = 1;		//全局变量,不建议在局部作用域中定义全局变量,导致维护困难

var message = “hi”,
   found = false,
   age = 29;

简单数据类型:Undefined,Number,String,Boolean,Null
复杂数据类型:Object

typeof message
return:undefined/boolean/number/string/object/function

typeof null  //return:object

null == undefined	//true

```
|数据类型| 转换为true的值|转换为false的值|
|:------:|:-------------:|:-----:|
|Boolean|true|false|
|String|任何非空字符串|" "(空字符串)|
|Number|任何非0数字值(包括无穷大)|0和NaN(Not a Number)|
|Object|任何对象|null|
|Undefined|n/a(not applicable)|undefined|

```JavaScript
var octalNum = 070 //八进制56
var hexNum = 0xA  //十六进制16

var floatNum1 = 1. //解析为1
var floatNum2 = 2.0 //解析为2

alert(NaN == NaN) //false
alert(isNaN(NaN)) //false
alert(isNaN(10))  //false
alert(isNaN("10"))  //false
alert(isNaN("red")) //true
alert(isNaN(true))  //false

var num1 = Number(false); //0
var num2 = Number(null); //0
var num3 = Number(undefined); //NaN
var num4 = Number(070); //56
var num5 = Number("070"); //70
var num6 = Number(" "); //0
var num7 = Number("0xA"); //10
var num8 = Number(new Object("2.2")); //2.2
var num9 = Number(new Object()); //NaN

var num1 = parseInt("1a") //1
var num2 = parseInt(" ")  //NaN
var num3 = parseInt("2.2")  //2
var num3 = parseInt("070", 8) //56

var num1 = parseFloat("1a")   //1
var num2 = parseFloat("1.1.1")  //1.1

alert("陈".length) //1

null.toString();  //null has no properties
undefined.toString(); //undefined has no properties

var num = 10;
num.toString(16);  //a

var value1 = true,
    value2 = null,
    value3;
alert(String(value1)) //true
alert(String(value2)) //null
alert(String(value3)) //undefined
```

#### 2.函数

函数没有重载，定义了两个相同名字的函数，该名字只属于后定义的函数。
可使用判断传入的参数个数作出不同反应，来模仿重载。
```JavaScript
function add(){
  var count = arguments.length;
  if (count == 1) {
    //相应操作
    alert(arguments[0]);
  } else if(count == 2){
    //相应操作
    alert(arguments[0] + arguments[1]);
  }
}
```
函数都用过值传递
```JavaScript
function setName(obj){
  obj.name = "Nick";
  obj = new Object();
  obj.name = "Tom";
}
var person = new Object();
setName(person);
alert(person.name); //Nick
```

#### 3.引用类型
```JavaScript
var person = new Object();
person.name = "nick"  // 动态属性
//该对象或该属性不被删除，该属性将一直存在。

var tom = "tom";
tom.age = 24;
alert(tom.age); //undefined
//不能为基本数据类型添加属性

instanceof
arr instanceof Array  //变量arr是否为Array

```
#### 4.变量、作用域和内存问题
JavaScript没有块作用域
```JavaScript
if(true){
  var a = 1;
}
alert(a); //1

var color = "red";
function getColor(){
  return color;
}
alert(getColor());  //red
//return color现在当前环境搜索，若没有再在上一环境搜索
```

#### 5.引用类型
##### 5.1 Object类型
创建对象
```JavaScript
//方式一
var person = new person();
person.name = "Tom";
//方式二
var person = {    
  "name" = "Tom";
}

person["name"]
person.name
```
##### 5.2 Array类型
```JavaScript
var arr = new Array(1,2,3);
var arr = [1,2,3];

arr[3] = 4; //新增第四项

alert(arr.length) //4

arr[arr.length] = 5; //新增第五项为5

arr.length = 6;
alert(arr[5]); //undefined

arr.length = 4;
alert(arr[3]); //undefined

Array.isArray(value) //检测数组方法

var colors = ["red", "blue", "green"]
alert(colors.toString());         //red,blue,green
alert(colors);                    //red,blue,green
alert(colors.valueOf());          //red,blue,green
alert(Array.isArray(colors.valueOf())); //true
alert(colors.toLocaleString());   //red,blue,green
alert(colors.join("|"));          //red|blue|green

var count = colors.push("yellow","black"); //5
var item1 = colors.pop()  //black, colors.length = 4
var item2 = colors.shift()  //red, colors.length = 3
```
