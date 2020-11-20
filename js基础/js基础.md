

# JavaScript是一种轻量编程语言

# 引入方式

- 内嵌式   在HTML内部 用<script></script>标签  
- 外链式   在HTML页面外部 存在一个.js文件 
- 行内式   不用

# 注释

- 单行   //
- 多行  /*   */

# 数据类型

- 基本数据类型   undefined null number Boolean string
- 复杂数据类型/引用数据类型  object function array

# 数据命名和存储

- 命名  
  - 不能以数字开头
  - 要语义化
  - 一般驼峰,命名
- 存储
  - 简单数据类型 存储在栈中 占据空间小 大小比较稳定
  - 复杂数据类型 存储在碓中  在栈中存储的是对应存储在碓的地址 通过操作地址 来操作负责数据类型

# 检查简单数据类型

```js
----typeof
    var a = 1;
	typeof a
// 特殊  typeof null  返回object
```

# 类型转换

- 转数字(number)
  - Number(数据)
    - '3000' ------> 3000
    - '3000ac' -----> NAN
    - 'sads' -------> NAN
    - true -------> 1
    - false ------->0
    - NAN 属于number 意思是 不知道是哪个数字
  - parseInt(数据)
    - 只有前面是数字的会转为前面的数字 整数  其余全部为NAN
  - parseFloat
    - 同上  但能取得小数
- 转字符串(string)
  - String(数据)
  - 数据.toString()方法
    - null 与 undefined 不能使用该方法  因为null和undefined只是原始值不是对象无法调用Object.toString()方法
- 转布尔值(Boolean)
  - Boolean(数据)
  - 为false的情况
    - undefined  null  ""  ''   ''   0  NAN   没有传入时参的形参 没有return 默认return
  - 为true
    - 特殊 空数组  空对象

# 操作符

- 算数操作符
  - 隐式转换  * - / % 都会把变量隐式转换为Number
- 比较运算符
  -  ==  比较两边的值 值相等就相等  会发生隐式转换 == 两边会转换成Number类型比较
  - ===  首先比较数据类型是否相等 如果不相等就不相等 如果相等比较值 值相等就相等
  - NAN != NAN  判断是否为NAN isnan(数据)
- 逻辑运算符
  - 且 &&
    - 必须两边条件都满足才为true 否则为false
  - 或 ||
    -  两边只要有一个为true就是true 两个为false才为false
  - 取反 !
    - !true === false
- 赋值运算符
  - = 
    -  var a = 5
- 优先级
  - () > 计算 > 比较 >逻辑

# 条件分支

- if语句

```js
if(a){
    // 代码1
}
else(b){				// 条件a 为true执行代码1  条件b 为true执行代码2 **** 否则执行else里代码
    // 代码2
}
....
else{
     // 代码n
}
```

- switch - case语句

````js
switch(key){       // key即将要传入的参数,判断的数据
    case value:			// case 情况   value 固定值  key === value 执行语句1
        语句1
        break; 		// break 结束判断
    case value1:
        语句1
        break;
    default      // 默认的
        break;
}
````

- 三元表达式

```js
表达式1?表达式2:表示式3
表达式1结果为true 执行 表达式2
表达式1结果为false 执行 表达式3
```

# 循环语句

#### 原生的js循环

- while循环

````js
while (条件) {
    语句
}
// 如果条件为true 则一直执行语句
````

- do  while 循环

````js
do {
    语句
}
while(条件);
// 先运行一次 再判断条件 
````

- for循环

````js
var arr = [1,2,3,4,5];
for(var i = 0; i<arr.length;i++){
    语句
}
    //执行顺序   i=0 执行 然后 i++ 然后判断 i<arr.length
````

- for in 循环

````js
var obj = {a:1 , b:2, c:3}  // 一般用于循环遍历对象
for(var key in obj){
    key 是 键名
    obj[key]是 键值
}

注意: 任何对象都继承了Object对象或者其他对象,继承的类的属性默认是不会遍历的,for in 循环遍历的时候会跳过,但是这个属性是可以更改为可以遍历的,那么就会造成遍历到不属于自身的这个属性
举例来说，对象都继承了toString属性，但是for...in循环不会遍历到这个属性。
var obj = {};// toString 属性是存在的obj.toString 
// toString() { [native code] }
for (var p in obj) { 
     console.log(p);
} // 没有任何输出
如果继承的属性是可遍历的，那么就会被for...in循环遍历到。但如果只想遍历自身的属性，使用for...in的时候，应该结合使用hasOwnProperty方法，在循环内部判断一下，某个属性是否为对象自身的属性。否则就可以产生遍历失真的情况。
var person = { name: '老张' };
for (var key in person) {  
    if (person.hasOwnProperty(key)) {   
         console.log(key);
      }
}// name
````

- map()循环：

````js
map方法将数组的所有成员依次传入参数函数，然后把每一次的执行结果组成一个新数组返回。
返回的是一个新数组 不会改变原数组
var arr = [1,2,3];
var arr1 = arr.map(function(n){
    returen n+1; 
})
console.log(arr) [1,2,3]
console.log(arr1) [2,3,4]

map方法接受一个函数作为参数。该函数调用时，map方法向它传入三个参数：当前成员、当前位置和数组本身。
var arr = [1,2,3]
var arr1 = arr.map(function(ele,index,arr){
    ele 当前成员
    index 当前位置
    arr 数组本身
})
map()循环还可以接受第二个参数，用来绑定回调函数内部的this变量，将回调函数内部的this对象，指向第二个参数，间接操作这个参数（一般是数组）。
var arr = [a,b,c]
[1,2].map(function(ele){
    return this[ele]
},arr)
// [b,c]
````

- forEach循环

```js
forEach方法与map方法很相似，也是对数组的所有成员依次执行参数函数。但是，forEach方法不返回值，只用来操作数据。也就是说，如果数组遍历的目的是为了得到返回值，那么使用map方法，否则使用forEach方法。forEach的用法与map方法一致，参数是一个函数，该函数同样接受三个参数：当前值、当前位置、整个数组。

// 要是操作原数组就用forEach 不要操作原数组就用map
```

- filter()过滤循环

````js
filter方法用于过滤数组成员，满足条件的成员组成一个新数组返回。它的参数是一个函数，所有数组成员依次执行该函数，返回结果为true的成员组成一个新数组返回。该方法不会改变原数组。
[1, 2, 3, 4, 5].filter(function (elem) {
     return (elem > 3); 
}) // [4, 5]
 
// 上面代码将大于3的数组成员，作为一个新数组返回。
 
var arr = [0, 1, 'a', false]; 
arr.filter(Boolean) // [1, "a"]


--------------------------------------------
filter方法也可以接受第二个参数，用来绑定参数函数内部的this变量。

var obj = { MAX: 3 }; var myFilter = function (item) {
     if (item > this.MAX) return true; 
}; 
var arr = [2, 8, 3, 4, 1, 3, 2, 9]; 
arr.filter(myFilter, obj) // [8, 4, 9]
上面代码中，过滤器myFilter内部有this变量，它可以被filter方法的第二个参数obj绑定，返回大于3的成员
````

#### 关键字

- break  continue

````js
break 终止循环
continue 终止本次循环 后面的代码不再执行
````

# 数组

- 声明-储值

````js
// 数组 
	1. 数组内可以存放任意类型的值
    2. 数组元素不赋值为undefined
    3. 打印数组时, 如果某个元素没有赋值 则为""
	4. 访问数组范围以外的元素时, 不会出现越界异常, 为undefined
	5. 定义数组大小, 依然可以添加更多的元素
var arr = [1,2,3,4];
var arr = new Array(1,2,3,4)
// 数组长度属性  arr.length

````

- 排序

````js
1. 冒泡排序
2. 插入排序
3. 快速排序
4. 选择排序
````

# 函数

- 创建函数方式

```js
//================================== 函数声明
function fn (a,b){
    console.log(a+b);
}
fn(3,4);  // 能够在任何地方调用 函数声明提前
//=================================== 函数表达式
var fn = function(a,b){
    console.log(a+b);
}
fn(3,4) // 只能在函数表达式后面调用因为变量声明提前
//==================================== 函数构造法, 参数必须加引号
var fn = new Function('a','b''return a+b) 
                      // 这是一个函数表达式 这种语法会解析两次代码 第一次解析ECMAScript代码, 第二次是解析闯入构造函数的字符串
```

- 参数配置

````js
// 参数是函数内部的变量 如果不传入时参 默认会得到undefined
// 时参与形参一一对应
// 如果在调用函数后, 希望得到一个结果, 需要在声明函数的时候, 设置return
//=================================================return
// 1.函数内部遇到return 后面代码不会执行
// 2.有return 且return后面有数据 则函数执行之后返回这个数据'
// 3.有return 但是return后面没有数据, 函数执行后返回undefined
// 4.没有return 函数执行后返回undefined
//==================================================遇到undefined
// 1.var a; 声明变量但是没有赋值
// 2.函数内部形参不赋值
// 3.获取数上没有被赋值的下标的值
// 4.函数内部设置return 后面没有数据  函数内部没有设置return
````

- 内置对象 date(获取时间)

````js
var date = new Date();
var year = date.getFullYear() // 年
var month = date.getMonth()+1 // 月
var day = date.getDate() // 日
var hover = date.getHours() // 小时
var minute = date.getMinutes() // 分钟
var second = date.getSeconds() // 秒
````

- 参数  arguments

```js
// 如果不确定 传入函数内部多少值 函数内部有隐藏变量arguments参数来接收  是一个伪数组
```

- 立即执行函数

````js
function(){}  这种形式不能单独出现在js中
立即执行函数
写法1.(function(){console.log(1)})(); 页面一打开就执行
自执行函数严格来说也叫函数表达式，它主要用于创建一个新的作用域，在此作用域内声明的变量，不会和其它作用域内的变量冲突或混淆，大多是以匿名函数方式存在，且立即自动执行。
写法2. ! function(){console.log(1)}();
````

# javascript 作用域

````js
// 全局作用域 
// 局部作用域  函数内部的作用域

//=======================================================
 // 作用域链 
 // 当在一个函数内部找一个变量时,首先看自己作用域有没有定义这个变量 如果没有则往上层作用域寻找 直到全局作用域

// with语句  
		主要用来临时扩展作用域链, 将语句中的对象添加到作用域的头部

// 例
	var person = {
        name : '张三',
        age : 16,
        sex : '男',
        with : {
        	name : '李四'
        }
    }
    with(person.with){
		console.log(name)
        // 此时name 为李四  with将person.with添加到当前作用域的头部,所以输出李四
        // with语句结束后, 作用域链回复正常
    }
    
````

- js预解析

```js
js 解析过程分为两个阶段 1.编译阶段 2.执行阶段
1.编译阶段就是预解析阶段, 在这个阶段js解释器把js脚本代码转换到字节码
2.执行阶段,在编译阶段js解释器借助执行环境把字节码生成机械码, 顺序执行

编译阶段(预解析阶段) 执行操作
var function 声明的变量提升 只是提前声明 不提前赋值  提升只是提升到当前作用域顶端 而不是都提升到全局

```

# 对象

- 创建对象方式

```js
=================================字面量
var obj = {
    // 添加属性和方法   键值对
    name : '张三',
    like : function(){
        consolo.log('打游戏')
    }
}
// 对象.值||匿名函数
obj.sex = '男'
obj.dislike = function(){
    console.log('睡觉')
}
// 对象[位置名] = 值||匿名函数
obj['age'] = 15 
=================================使用new实例化构造函数对象
var obj = new Object();
obj.name = '张三';
obj.like= function(){
	consolo.log(111)	
}
-----------------------------------------------------------------------------------------
    new关键字的执行过程   1.创建一个空对象
    				   2. 将构造函数作用域赋值给新对象(改变了this指向)
                       3. 执行构造函数的代码(为这个新对象添加属性方法)
					   4. 返回这个新对象
    
-----------------------------------------------------------------------------------------

================================= 自定义构造函数       
1)无参
function ob(){   
}
var ob = new ob();
}
ob.name = '张三';
ob.like = function(){
    
}
2)有参
function Obj(name,like){
	this.name = name;
    this.like = function(){
		console.log(11)
    }
}
var obj = new Obj('张三');
obj.like()
=================================工厂模式 
function obj(name){
    var o = new Object();
    o.name = name;
    o.getname = function(){
		return this.name;
    }
    return o;
}
var obj1 = obj(1)
var obj2 = obj(2)
=================================混合模式(原型和构造函数)
functon obj (name,age){
    this.name = name;
    this.age = age;   // 构造函数内部放属性
}
obj.prototype.like = function(){   // 原型对象上放方法
	console.log(1111)	
}
var obj = new obj('张三',12)
```

- 遍历对象

```js
var obj = {
    name : '张三',
    age : 12,
    sex : '男',
    like : function(){
        console.log(111);
        
    }
}
//------------------------------------------ for in 
for(var key in obj){
    console.log(key+':'+obj[key]);
    // key 为对象位置名 
    // obj 原对象
}
//------------------------------------------ Object.keys()
Object.jeys(obj).forEach(function(key){
	console.log(key,obj[key]);	
})
```

- 内置对象-Math

````js
var number = Math.random();  // 获取一个[0,1)的随机数
Math.floor(number)  // 向下取整
Math.ceil(number)  // 向上取整
Math.abs(number) // 取绝对值
Math.max() // 取最大值
Math.min() // 取最小值
Math.round() // 四舍五入


-----------------------------------------------取n-m之间的随机整数
Math.floor(Math.random()*(m-n)+n+1);
````

- 内置对象-时间对象 new Date();

````js
// ------------------------------------------------------------获取时间戳
  var time = new Date(); //构造出时间对象；
  // 获取 时间距离1970 1 1 毫秒数，时间戳
	
  // 获取只是当前时间的时间戳
  // console.log(Date.now());

 // --------------创建一个**指定日期**的对象：那么这些对象也可以使用上面的方法；
 // 给一个日期格式字符串
var date = new Date('2019-01-01');

// 分别传入年月日时分秒。注意传入的月份是从0开始算的
var date = new Date(2019,0,1,12,33,12);
````

# 简单数据类型与复杂数据类型

````js
简单数据类型 null undefined number string Boolean
复杂数据类型(引用数据类型) function array object
简单数据类型数据存储在栈中
复杂数据类型数据存储在碓中 但是声明放在栈中 栈中放的是复杂数据类型的地址 
````

# 数组内置方法

````js
pop  
// 从后删除一项元素 
// 无参数
// 返回这个被删除的元素的值  改变原数组
push
// 从后添加一个或者多个元素
// 参数一个或者多个元素
// 返回数组改变后的长度值length 改变原数组
unshift
// 从数组开头添加一个或者多个元素
// 一个或这多个元素
// 返回数组改变后的长度值length 改变原数组
shift
// 从数组开头删除一个元素
// 无参数
// 返回这个删除的值 改变原数组

splice
// 对数组任意位置进行 增删改

// 在数组任意位置增加一个或者多个元素
// 参数:
	参数1: 从哪个下标开始
    参数2: 0 没有要删除的个数
    参数后面: 要添加的成员
// 返回 [] 空数组  改变原数组
    

// 数组任意位置删除一个或者多个元素
// 参数:
    参数1: 从哪个下标开始
    参数2: 要删除的个数
// 返回 被删除元素的数组  改变原数组
 
    
// 数组任意位置的替换
// 参数
    参数1: 从哪个下标开始
    参数2: 要被替换元素的个数
    参数后面: 要替换的值
// 返回 被替换元素的数组  改变原数组
    
    
slice  //截取数组
	//参数
		参数1. 从哪个下标开始
		参数2  到哪个下标结束 不包括这个下标
    // 返回 截取的数组
    // 不改变原数组
 join // 把数组按照特定格式转换为字符串
	  // 参数 按照哪种特殊格式(,)或者(?)
 	  // 返回值 被特定格式转换后的字符串 不改变原数组
 indexOf() // 查询一个元素是否在数组内
			// 参数: 要查询的元素
			// 返回 有就返回当前数据在数组中下标 没有返回-1
 findIndex() // 查询一个元素在数组内的下标
			 // 参数: 匿名函数
					形参: 数组中的每个成员, 内部变量 item
					必须这样设置 return 查询条件
			// 返回 第一个满足条件成员的下标
var arr = [1,56,76,8879,9,8]
var res = arr.findIdex(function(item){
    return item >1000;
})
console.log(res);
concat // 拼接数组
		// 参数 要拼接的数组或者单个数据 一个或者多个
		// 返回 拼接后的新数组 不会改变原数组
````

# 字符串内置方法

````js
split // 把字符串按照特定格式转换为数组
		// 参数 规定按照哪种格式转换例如(',')
		// 返回转换的数组  不会改变字符串
// 面试题：参数：解析为对象形式  
var str = "http:xxx.xxx.com?name=zs&ps=aaa&info=abc";
// 思路 1.利用split()分割字符串为数组然后取得需要的字符串
	//  2. 最后循环添加到对象里 
var res = str.split('?')[1].split('&');
console.log(res);

var obj ={};
for(var i = 0; i<res.length;i++){
    var one = res[i];
    obj[one.split('=')[0]] =one.split('=')[1];
}
console.log(obj);
charAt
  // 找到指定下标那个字符； 
  // 参数：指定下标
  // 返回：找到字符串；

  // length：获取字符串里字符的长度：
// 统计字符串里面出现次最多的字符,以及出现了几次
var str = 'sdsdhgfasdfkadsasdadsadsaddqeadfeadfsa';
// 思路 : 
// 1. 准备一个空对象
// 2. 循环获取每一个字符 把这个字符当成对象属性 
// 3. 如果该对象没有这个属性 则加上这个属性 并让值为1  视为该字符串第一次出现
// 4. 对象如果有这个属性 则为第二次出现 让该对象值+1  对象里面会存储 字符串:他的出现次数
// 5. 遍历对象 比较出最大值 也就是出现次数最多的
var obj = {};
for(var i =0;i<str.length;i++){
    var one = str.charAt(i);
    obj[one] === undefined? obj[one] = 1:obj[one]+=1;
}
console.log(obj);

var max = 'a';
var max_index = 5;
for(var key in obj){
    if(obj[key]>max_index){
        max = key;
        max_index = obj[key]
    }
}
console.log(max,max_index);

concat 字符串拼接
		// 参数 一个或者多个字符串
		// 返回一个新字符串
		// 不改变原来字符串
substring：
	字符串截取，不操作原字符串
  		参数：
           1：从哪个下标开始  可以省略
           2：到哪个下标结束  （包左不包右） 可以省略
   返回：截取出来字符串；不操作原字符串
 slice  字符串截取，不操作原字符串
   参数：
         1：从哪个下标开始  可以省略   可以写负值
         2：到哪个下标结束  （包左不包右）  可以省略
    	返回：截取出来字符串；不操作原字符串；
 substr: 字符串截取，不操作原字符串
 	参数:
		1. 从哪个下标开始  可以省略
        2. 截取几个 可以省略
    返回：截取出来字符串；不操作原字符串；
````

