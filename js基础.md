# Object类

###  基础用法

```javascript
1.var person =new Object(); //var person={};意思相同
person.name="Ni";   
person.age=20;   
//person["name"] (这是js特有语法，上同)
//[]由于内部是String类型，但是属性名是不可以为非字母非数字的
2.var person ={
    name:"Ni",
    age:20
};
```

# Array类

标注：ECMAScript数组可以存放如何类型的数据  （数组最大为4294967295）

### 基础用法

```javascript
//上面三种都可以省略new
1.var colors=new Array();
2.var colors=new Array(20); //长度为20的数组
3.var colors=new Array("green");//包含一项为green的colors数组

4.var colors=["red","blue","green"];//包含了red、blue、green的colors数组
5.var colors=[];//空数组
//访问数组可以通过index => arr[index]

//通过更改已有数组的length，可以将之后访问会变为undefined
var p=["n","m","l"];

p.length=4;
p[3] //第四个元素为undefined

p.length=2;
p[2] //原有的p[2]也变为undefined
```

### 检测数组（instanceof,isArray）

```java
//ES3
//用于检测构造函数的 prototype 属性是否出现在某个实例对象的原型链上。
if(value instanceof Array){
    //对数组执行某些操作
}
//全局环境下多种框架的构造Array函数不同而受影响

//ES5(为了解决上方问题)
if(Array.isArray(value)){
    //对数组执行某些操作
}
//目的是确认是否为数组
```

### 转换方法( "toLocaleString()"," toString()","valueOf()")

```javascript
//toLocaleString(), toString(),valueOf()  所有对象都有这个方法

var colors=["red","green","blue"];
colors.jion(","); //red,green,blue
colors.jion("||"); //red||green||blue
```

### 栈方法（后进先出）

```javascript
//push(),pop()
var colors=[];
var count=colors.push("red","green","blue"); //3
colors.length; //3

colors.pop(); //blue(最后一项)
```

### 队列方法（先进先出）

```javascript
// shift(),pop()
//与其相反的是unshift()
var colors=[];

var count=colors.shift("red","green","blue");
colors.pop();//red(第一项)

var count=colors.unshift("red","green","blue");
colors.pop();//red(最后一项)
```

### 重排序方法

```javascript
//这两种都会直接改变原有数组
reverser()  //直接反转数组
sort()  //排序，会调用每个数组项的toString()所以进行的是String的比较方法

//可以调用其他函数的方式完成排序
let c=[0,1,2,13,8,-1];
        c.sort();
        c.sort((value1,value2)=>{
            if(value1<value2){
                return -1;
            }else if(value1>value2){
                return 1;
            }else{
                return 0;
            }
        })
//[-1, 0, 1, 2, 8, 13]
```

### 操作方法

#### concat() 

 数组中添加其他的值或数组（多个）,形成一个新的数组

```javascript
//不会改变原有函数
var colors=["red","green"]; 
var colors2=colors.concat("yello",["black","brown"]); //red,green,yello,black,brown
```

#### slice()

传入值有一个或者两个，一个是起始位置还有一个结束位置。它会将取出的数组项转为一个新的数组

```javascript
var colors=["red","green","yello","black"];
var colors2=colors.slice(2); //[yello,black]，从index为2的开始到结束
var colors3=colors.slice(1,2); //[green,yello]

//可以进行输入负数
//原数组长度为5
slice(-2,-1) == slice(5-2，5-1) == slice(3,4)
```

#### splice()

基本用法：splice(起始位置,删除个数,[添加的元素])
提供了删除，插入，替换3中方法(会改变原数组)

```javascript
//删除
splice(0,2) //删除从第0位置的开始删除两个，他返回的是一个数组
//插入
splice(2,0,"red","green") // 从第2位置的开始插入"red""green"
//替换
splice(2,1，"red","green") // 从第2位置的开始,删除一个元素,插入"red""green"
```

### 位置方法

#### index()和lastIndexOf()

两者传值都是(查找元素，起始位置的index)
都是寻找第一项后直接返回index,未找到返回-1

### 迭代方法

//es5

五种迭代方法，**方法的接受参数**：函数   ，作用域对象（可选）——影响this的值。**内部函数**：传入参数有三个分别是：数组项的值，数组项的index，数组对象本身

```javascript
var numbers=[1,2,3,4,5];

//五种迭代方法基本用法拿个every()打比方
number.every(function(item,index,array){
    return (item>2)
})
//上同
number.every((item,index,array)=>{
	return (item>2);
});
```

#### every()

运行指定函数，运行结果都为true才会返回true;（判断,结果boolean）

#### some()

运行指定函数，运行结果只有有一个true就会返回true（判断,结果boolean）

#### filter()

运行指定函数，运行结果是每一项都为判断结果为true的一个数组（判断,结果array）

#### map()

运行指定函数，运行结果是数组中所有的数组项都根据函数计算后的一个数组（计算,结果array）

#### forEach()

运行指定函数，没有返回值（计算，无返回值）

### 归并方法

es5新增两种归并方法：**reduce()**和**reduceRight()**

**共同点：**都会迭代数组的所有项

**基本用法：**接受两个参数（给每一项调用的函数，(可选)作为归并基础的初始值）

内部函数结束最多4个参数：（前一个值，当前值，项的索引，数组对象）

```javascript
let values=[1,2,3,4,5];
//第一次运行数组的前两个值，之后prev都是return结果
let sum=values.reduce(funtion(prev,cur,index,array){
                      return prev+cur;
                      })
console.log(sum);//15
//reduceRight就是从数组的尾部开始取值与reduce相反
```

# Date类

### 基本用法

```javascript
var date=new Date();//没接受参数就返回当前系统时间

//在传参数的情况，提供两种:Date.parse() <默认的>和Date.UTC()

//Date.parse() 接受参数:一个日期格式的字符串
//ES5新增YYYY-MM-DDTHH:mm:ss.sssZ(如2004-5-25T00:00:00)
var date=new Date("May 25,2004"); ==  var date=new Date(Date.parse("May 25,2004"));

//Date.parse() 接受参数（至少参数年月）：年，月（0-11），日（1-31），小时，分钟，秒，毫秒(基于系统时间的本地去创建而不是GMT来创建)
var date=new Date(Date.UTC(2005,4,5,17,55,55));
//对应时间：2005年5月5日17：55：55
```

### ES5新增 Date.now()

用途：查看代码运行的时间，分析代码的工作

```javascript
var start =Date.now();
//调用函数
doSomething();
var stop =Date.now(),result=stop-start;
```

# RegExp类型

### 基本用法

```javascript
var exp= /pattern/flags;
//pattern 任意的正则表达式
//flags 可以存在一个或者多个，标明正则表达式的行为
```

###  六种标明行为（i,g,m,y,u,s）

**g:**表示全局模式(global)，在找到第一个匹配对象后不会直接停止

```javascript
/at/g;
//找到所有为at的实例
```

**i:**表示不区分大小写(case-insensitive)模式，寻找匹配的第一个字符串

```javascript
/[bc]at/i;
//找到第一个bat或者是cat的，不区分大小写
```

**m:**表示多行（multiline）模式,找不到会进行下一行的搜索

**y:**粘附模式，展示**只**找lastIndex及以后的字符串

**u:**Unicode模式，开启Unicode匹配

**s:**dotAll模式，表示元字符.匹配任何字符（包括\n或\r）



### **正则表达式的元字符：（   [   {   \   ^  $  |  )  ?  *  +  .  ]  }  ）**

转义会需要在这些元字符和其他正则表达式（如\w,\d）的前面加上再多加上一个“\”

####  RegExp() 的实例及属性

```javascript
var parttern=/\[bc\]at/i;

//第一个参数的是/.../之间经过转义的原正则表达式，第二个参数是i,g,m模式
var parttern=new RegExp("\\[bc\\]at","i");
```

### 属性(不是方法是属性！！！)

##### global

判断是否设置g模式，返回boolean

##### igonreCase

判断是否设置i模式，返回boolean

##### multiline

判断是否设置m模式，返回boolean

##### unicode

判断是否设置u模式，返回boolean

##### sticky

判断是否设置y模式，返回boolean

##### dotAll

判断是否设置s模式，返回boolean

##### lastIndex

表示开始搜索下一个匹配项的字符位置，0算起

##### source

正则表达式的字符串表示，输出的是转义完成前的表达式

##### flags

返回正则表达式后面的模式的字符串

### RegExp实例方法

#### exec()方法

即使设置了全局模式（g）,它**每次**也只会返回一次匹配项。不是全局模式多次调用会返回都是第一个项，全局模式会继续寻找新的匹配对象，原因是全局模式下pattern的lastIndex属性每次都会增加，而非全局模式保持不变。

```javascript
let text="mom and da and bady";
//?是捕获组的
let pattern=/mom(and dad(and bady)?)?/gi;

//现在match是一个数组array实例,而现在match现在有两个属性：index和input
//index：匹配项的在字符中的位置
//input: 原正则表达式
let match=pattern.exec(text);
match.index==0 //因为这个字符串本身与这个字符串匹配

//上面运行过程：第一项匹配整个字符串 > 在第一项的基础上匹配第二项 > 在第二项的基础上找第三项
```

#### test()方法

返回boolean,用在判断条件上

#### toString(),toLocaleString(),valueOf()方法

toString()和toLocaleString()都是返回正则表达式的字面量

valueOf()返回正则表达式的本身

### 九种存储捕获组

RegExp.$1 到RegExp.$9

```javascript
var text="this has been a short summer";
var pattern=/(..)or(.)/g;

//构造函数属性会x被匹配相应捕获组的字符串进行自动填充
if (pattern.test(text)){
	alert(RegExp.$1); //sh
    alert(RegExp.$2); //t
}
```

# Symbol类(es6)

### 基本用法

```javascript
//没有new,而且唯一
let sym=Symbol("sym"); //非全局

console.log(typeof sym);//symbol

let sym1=Symbol.for("sym1"); //全局，第一次寻找有没有定义的sym1标志，没有就会创建，如果有会返回之前创建的那个实例
Symbol.keyFor(sym1); //sym1 ,查询全局注册表，如果不是全局的会返回undefined


```

### 符号作为属性

#### 基础用法

```javascript
let s1=Symbol.keyFor("foo");
let	o={
	[s1]:'foo val';
}
```

#### Object.defineProperty()

```javascript
let s2=Symbol.keyFor("bar");
let o={};
Object.defineProperty(o，s2,{value:"bar val"});
```

#### Object.defineProperties()

```javascript
let s3=Symbol.keyFor("baz");
let s4=Symbol.keyFor("qux");
let o={};
Object.denfineProperties(o,{
    [s3]:{value:"baz val"},
    [s4]:{value："qux val"}
});
```

#### Object.getOwnPropertyNames()

返回常规属性的一个数组

#### Object.getOwnPropertySymbols()

返回symbol类型为属性的一个数组

#### Object.getOwnPropertyDescriptors()

返回包含常规和symbol属性描述符的对象

#### Reflect.ownKeys()

返回两种类型的键

### 内部符号（@@）作用重构

#### Symbol.hasInstance

```javascript
//自定义的instanceof
class MyArray {
  static [Symbol.hasInstance](instance) {
    return Array.isArray(instance);
  }
}
console.log([] instanceof MyArray); // true
```

# String类(es6新增)

### 反引号（``）

内部用${变量} ，变量会自动填充并强制调用toString()

### 原始字符串

String.raw属性

