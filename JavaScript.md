## js
### ES5和ES6的区别
功能类别 | ES5 | ES6（ES2015）
---|---|---|
变量声明 | var | let, const
作用域 | 函数作用域 | 块级作用域（let 和 const）
字符串拼接 | 'Hello ' + name | 模板字符串：`Hello ${name}`
函数参数默认值 | 手动处理：`x = x | 
箭头函数 | 无 | const fn = () => {}
对象属性简写 | {name: name} | {name}
对象方法简写 | sayHi: function() {} | sayHi() {}
构造函数与类 | 用函数构造器模拟类 | class 和 constructor
继承 | 原型链手动继承 | class A extends B
模块化 | 无内建模块系统，需用 CommonJS | 内建模块化 import/export
解构赋值 | 无 | const {x, y} = obj / [a, b] = arr
展开运算符 | 无 | ...arr, ...obj
Promise | 不支持 | 支持异步编程 Promise
Set/Map | 无 | 原生支持
Symbol | 无 | 新增基本类型 Symbol
for...of循环 | 无 | 遍历可迭代对象
模块引入机制 | require()（Node.js） | import / export（原生支持）
生成器函数 | 无 | function* 与 yield

**补充：**
- `let` 和 `const`解决的 `var` 存在的变量提升、作用域污染问题；
- `箭头函数`绑定的词法作用域的`this`，不会被调用方式影响；
- `模板字符`串支持多行字符串以及表达式插值，提升代码可读性；
- 模块化是前端工程化的基础，ES6的`import/export`让代码更加清晰、更容易维护；
- `Promise`是异步编程改革的起点，为后续的`async/await`铺路；
- `Set/Map`提供了更适合的场景下的数据结构选择。

### ES6简述module、export、import的作用
在ES6中，每个 `.js` 文件默认就是一个模块，模块内部定义的变量、函数、类，默认都是私有的，除非用export显式导出
- 模块功能取代了`CommonJS`和`AMD`规范
    - **AMD：** 异步模块定义，采用异步方式加载模块，所有依赖模块的语句，都定义在一个回调函数中，等到模块加载完成之后，这个回调函数才会执行
    - **ConmmonJS：** 模块是同步加载的，如果多次require，会缓存第一次的结果，并且require的是对象的拷贝，不是实时绑定

- **CommonJs**
CommonJs可以动态加载语句，代码发生在运行时
CommonJs混合导出，还是一种语法，只不过不用声明前面对象而已，当我导出引用对象时之前的导出就被覆盖了
CommonJs导出值是拷贝，可以修改导出的值，这在代码出错时，不好排查引起变量污染
- **Es Module**
Es Module是静态的，不可以动态加载语句，只能声明在该文件的最顶部，代码发生在编译时
Es Module混合导出，单个导出，默认导出，完全互不影响
Es Module导出是引用值之前都存在映射关系，并且值都是可读的，不能修改

**export的作用**——用于对外暴露模块内的变量/函数/类等

方式一：命名导出
```javaScript
//pi.js
export const PI = 3.14
```
方式二：默认导出
```javaScript
//math.js
export default function add(a,b){
	return a+b
}
```

**import的作用**——用于导入其他模块导出的内容
```javaScript
//utils
import {PI} from './pi.js'
import add from './math.js'
console.log(add(Pi,2))	//5.14
export const PI = 3.14
```
---
### ==和===的区别
`==` 判断值，如果类型不一样，将通过`valueOf()`进行隐式转换
```javaScript
console.log('123'==123)		//true
```

`===`不仅判断值还判断数据类型
```javaScript
console.log('123' === 123)		//false
```

`===`存在的一个问题
```javaScript
console.log(+0===-0)		//true
console.log(NaN===NaN)		//false
```
改良👇👇👇
```javaScript
console.log(Object.is(+0,-0))		//false
console.log(Object.is(NaN,NaN))		//true
```
---
### var let const 的区别
区别|var|let|const|
---|---|---|-----|
作用域|函数作用域，var声明的变量只在其所在的函数内有效，如果在函数外部声明，则为全局变量|块级作用域，只在其所在的代码块内有效|同|
变量提升|有，会被提升到函数和全局作用域的顶部，未初始化的变量在提升时为undefined|在声明前不能访问，会出现ReferenceError|同
重新赋值|可以|可以|不可以，在声明时必须初始化，但是如果是对象元素，内部的属性可以修改

---

### js中的转义符
- 特殊字符：换行符`\n`，制表符`\t`等，用于格式化输出；
- 在字符串中使用界定字符串的引号，如通过`\"`或`\'`来避免语法错误；
- 表示不可打印字符：如退格符`\b`，回车符`\r`等；
- 通过十六进制\x和Unicode（`\u`）转义序列表示特定字符
- ---

### js中的负无穷大是什么
在js中，负无穷大表示一个小于所有其他数值的特殊值，可以通过`let negativeInfinity = -Infinity`获得，`-Infinity`是一个内置的全局属性，代表负无穷大的值，常用于数据计算和浮点数运算中的边界情况
```javaScript
console.log(-1 / 0)    ///-Infinity
```
---

### 数组方法
**常用的数组方法有：**
|方法|作用|
|---|---|
|push|在数组的后面添加一个元素，返回新长度
|unshift|在数组前面添加一个元素，返回新长度
|pop|在数组尾部删除一个元素，返回被删值
|shift|在数组头部删除一个元素，返回被删值
|join|数组转化为字符串
|forEach|遍历每一个数组进行相应操作，没有返回值
|map|对每一个数组进行操作，并返回一个新数组
|reduce|对数组中的每一项一次执行某种操作，最终“规约”为一个值
|find|查找符合条件的值，并返回第一个符合条件的值
|filter|筛选的所有符合条件的值并返回
|some|判断是否有一个值符合条件，返回true/false值
|every|判断是否所有值都符合条件，返回true/false值
|slice|截取部分数组返回新数组
|splice|添加/删除/替换指定位置元素

#### 数组扁平化并去重
```javaScript
const arr = [1,2[3,4],[5,6,[7,8]],9,9,2]
//通过  数组.flat()方法进行扁平化处理，将多维数组转为一维数组
//inifinity参数用于递归扁平

const flattenedArr = arr.flat(infinity) 

const res = [...new Set(flattenedArr)]
```

#### 查找数组中重复出现次数最多的元素

```JavaScript
//思路：通过对象进行二次映射,数组元素->属性名，出现次数->属性值
function findMost(arr){
    let countMap = {}
    let mostCount = 0
    let freqitem = null
    arr.forEach((item) => {
        countMap[item] = (countMap[item]||0) + 1
        if(countMap[item]>mostCount){
            maxCount = countMap[item]
            freqItem = item
        }
    })
    return {
        item: freqItem,
        count: maxCount
    }
}

const arr = [1,2,1,3,4,2,2]
let most = findMost(arr)
console.log(`出现次数最多的元素是${most.item}，次数为${most.count}`)
```

#### 数组长度是10，删除第五个元素
```JavaScript
//方法一：使用splice()方法   推荐√ 
let arr = [1,2,3,4,5,6,7,8,9,10]
let arr1 = arr.splice(4,1)  //从index为4的地方开始，删除一个元素

//方法二：使用slice()+concat()

let brr = [1,2,3,4,5,6,7,8,9,10]
let brr1 = brr.slice(0,4).concat(brr.slice(5))
```
#### slice()和splice()
```JavaScript
let arr = [1,2,3,4,5,6,7,8,9,10]
//slice
let arr1 = arr.slice(0,4) //从下标0开始，不包括下标4，返回一个新数组
console.log(arr1)   //[1,2,3,4]

//splice
let arr2 = arr.splice(4,2)    //从下标为4，截取出来两个元素，改变原数组，返回删除的内容
console.log(arr2)   //[5,6]
console.log(arr)   //[1,2,3,4,7,8,9,10]
```
#### forEach()和map()

```JavaScript
//map()
const arr = ['a','b','c']
const brr = arr.map((item) => {
    return item + '1'
})
console.log(brr)   //['a1','b1','c1']

//forEach()
arr.forEach((item,index)=>{
    arr[index] = item + '1'
})
console.log(arr)   //['a1','b1','c1']
```

#### find()和filter()
```JavaScript
//find()
const arr = [1,2,3,4,5]
let res = arr.find((item) => {
    return item > 3
})
console.log(res)   //4

//filter()
const brr = arr.filter((item)=>{
    return item > 3
})
console.log(brr)   //[4,5]
```

#### some()和every()
```JavaScript
//some()
const arr = [1,2,3,4,5]
let res = arr.come((item) => {
    return item > 3
})
console.log(res)   //true

//every()
res = arr.every((item)=>{
    return item > 3   
})
console.log(res)   //false
```
----
### js中的freeze()方法的作用
`Object.freeze()`是一个用来冻结对象的方法，**冻结后的对象将不能添加、修改、删除属性，也不能修改原型，变成一个完全不可变的常量**，但是这种**冻结是浅层的**，嵌套对象内部还是可以修改
```javaScript
function deepFreeze(obj){
	Object.freeze(obj)
	for(let key in obj){
		if(typeof(obj[key])==='object' && obj[key]!==null){
			deepFreeze(obj[key])
		}
	}
}
```
---
### null、undefined
在最开始设计js语言时，借鉴Java，采用null表示“无”，但是null会被隐式转换为0，很不容易发现错误，因此提出了undefined
null→undefined
**具体区别：**
null表示一个“无”的对象（空对象指针），转为数值是0
```javascript
console.log(typeof(null))	//object
console.log(Number(null))	//0
```
undefined是一个表示“无”的原始值，转为数值是NaN
```javascript
console.log(typeof(undefined))//undefined
console.log(Number(undefined))//NaN
```
补充一个：undeclared（未声明）
`undeclared`指未声明的变量，尝试访问一个没有声明的变量会导致`referenceError`错误

<hr>

### typeof和instanceof的区别
typeof 用于判断数值类型，返回一个字符串，适用于原始数据类型
```javascript
console.log(typeof(typeof(null))	//String
```
instanceof 用于判断对象是否属于某个类的实例，适用于引用类型的判断
```JavaScript
//实现一个自己的instanceof,原理为原型链的向上查找
const instancesof = (traget,obj)=>{
	let p = target
	while(p){
		if(p == obj.prototype){
			return true
		}
		p =p.__proto__
	}
	return false
}
console.log(instancesof([1,2,3],Array))	//true
```
typeof无法准确判断引用类型，instanceof无法判断基本数据类型，如果想要通用的检查数据类型，可以使用Object.prototype.toString，该方法会统一返回格式为`[object xxx]`的字符串

```javaScript
//基于Object.prototype.toString实现通用类型判断
function getType(obj){
    let type = typeof obj
    if(type !== 'object')
        return type   //基本数据类型&function直接返回
    return Object.prototype.toString.call(obj).replace(/^\[object (\S+)\]$/, '$1')
}
```
<hr>

### sort是什么以及sort背后的原理
`Array.prototype.sort()`用来对数组元素进行排序，默认情况下，根据字符串的Unicode编码进行排序，不管传入的是数字还是字符，并且会出现不符合常理的情况，比如认为100<13

如果需要正常排序，传递一个比较函数作为排序规则：
```javaScript
arr.sort((a,b)=>a-b)
//返回负数（比如 -1）→ a 排在 b 前面
//返回正数（比如 1）→ b 排在 a 前面
//返回 0 → 保持原顺序（但注意并不保证是稳定的）
```
**背后原理：**
不同的浏览器底层实现不同，大致遵循以下几种排序算法：
小数组使用插入排序
大数组使用快速排序

<span style = 'color:red;'>注意：</span>
- 修改原数组
- 默认是不稳定的排序

---

### 判断变量是不是数组
```JavaScript
let arr = [1,2,3]
//方法一：Array.isArray()
console.log( Array.isArray(arr) )

//方法二：isPrototypeOf()：用于判断当前对象是否是另外一个对象的原型，是则返回true
console.log( Array.prototype.isPrototypeOf(arr) )

//方法三：constructor
console.log( arr.constuctor.toString().indexOf('Array') > -1 )

//方法四：Object.prototype.toString.call()——Object.prototype.toString本身就是一个方法，不用佳括号
console.log( Object.prototype.toString.call(arr) === '[object Array]' )

//方法五：instanceof()
console.log(instanceof(arr,Array))
```
---

### 任务队列中的宏任务以及微任务

异步任务进入任务队列的顺序是，先微任务后宏任务

**常见的微任务有：**
Promise的then()和catch()方法产生的回调
async/await中await关键字后面的代码

**常见的宏任务有：**
定时器的回调
事件监听的回调
I/O操作（文件读写、网络请求）的回调
渲染事件（requestAnimationFrame）的回调

---

### 什么是类数组，怎么将类数组转换为真正的数组
#### 1.是什么
类数组是一种类似数据的对象，但不是真正的js数组，其主要特点是：
- 具有length属性，表示类数组中元素的数量；
- 类数组可以包含从0开始的自然递增整数作为键名；
- 类数组可以向一个真正数组一样进行遍历，如使用for循环
- 不能使用真正的数组方法，如pop、push、forEach等

#### 2.怎么转换

```JavaScript
//Array.form(伪数组)
const lis = document.querySelector('ul li')
const arr = Array.from(lis)
```
---
### 数组去重
```javaScript
//集合去重再结构赋值
const arr = [1,2,3,4,2,1]
const uniqueArr = [...new Set(arr)]

//使用filter()以及indexOf()
const uniqueArr = arr.filter((value,index,self)=>self.indexOf(value)===index)

//使用reduce以及includes
const uniqueArr = arr.reduce((acc,cur)=>acc.includes(cur)?acc:[...acc,cur],[])

//双重循环
const uniqueArr = []
for(let i = 0;i < arr.length;i++){
	if(uniqueArr.indexOf(arr[i]) === -1)
		uniqueArr.push(arr[i])
}
```
---
### 什么是闭包

**定义**
闭包是指有权访问另一函数作用域中的变量的函数。当一个函数能够访问并记住在其外部函数作用域中定义的变量，即使外部函数已经返回，这些变量也依然存在，就形成了一个闭包。<b>核心思想：创建私有变量、延长变量声明周期</b>
_私有变量：外部可以通过一些方法访问内部的私有变量_

**优点**
- 记忆功能：闭包可以保存状态，如计数器、缓存等；
- 延长变量的生命周期：闭包是的变量的生命周期与函数的执行时间相关，而不仅在声明时；
- 实现高阶函数：闭包常用于创建柯里化函数或函数工厂

**缺点**
- 内存消耗：由于闭包会持有外部变量，可能会导致内存泄漏（IE浏览器中），尤其是在循环中创建大量闭包；
- 型能影响：闭包会增加代码的复杂度，导致额外的开销；
- 难以调试：闭包内部变量不易察觉，会影响代码的可读性和维护性

**使用场景**
- 模块化开发：通过闭包创建私有变量和方法，实现模块化的代码结构；
- 函数式编程：高阶函数、柯里化、延迟执行等场景
- 缓存和回调：如，实现异步操作的回调函数，可以用闭包保存状态
- 事件处理程序：在事件监听中，可以使用闭包存储与特定事件相关的状态；
- 计数器和迭代器：闭包可以用来维护循环中的状态，实现迭代器或计数器
```javaSCript
//通过闭包实现防抖函数
function debounce(fn,delay){
    let timer = null;
    return function(...args){
        const context = this
        clearTimeout(timer)
        timer = setTimeout(()=>{
            fn.apply(context,args)
        },delay)
    }   
}

```
---
### 作用域链
<span style = 'color:red;font-weight:bold;font-size:19px'>作用域</span>

作用域即变量（变量作用域又称上下文）和函数生效（能被访问）的区域和集合，作用域决定了代码区块中变量和其他资源的可见性
- **全局作用域**——任何不在函数或者大括号内中声明的变量，都可以在程序的任何位置访问
- **函数作用域**——一个变量在函数内部声明，那就只能在该函数内访问
- **块级作用域**——在大括号内通过let、const声明的变量存在于会计作用域内，大括号外不能访问

<span style = 'color:red;font-weight:bold;font-size:19px'>词法作用域</span>

词法作用域，又叫静态作用域，变量被创建时就确定好了，而非执行阶段确定的。也就是说我们写好代码时它的作用域就确定了
```javaScript
var a = 2;
function foo(){
    console.log(a)
}
function bar(){
    var a = 3;
    foo();
}
bar()   //   2，foo&bar是同级的，无法访问各自作用域内部的变量
```
<span style = 'color:red;font-weight:bold;font-size:19px'>作用域链</span>
在js中使用一个变量时，js引擎会尝试在当前作用域下寻找该变量，如果没有，到他的上层区域查找，依次类推直到找到该变量或者已经到了全局作用域，如果在全局作用域里仍然找不到该变量，它就会在全局范围内隐式声明该变量(非严格模式下)或是直接报错

---
### 执行上下文和执行栈
<span style = 'color:red;font-weight:bold;font-size:19px'>执行上下文</span>
执行上下文是一种对js代码执行环境的抽象概念，也就是说只要有js代码运行，那它就一定是运行在执行上下文中
- **全局执行上下文**
    只有一个，浏览器的全局对象就是window对象，this指向这个全局对象
- **函数执行上下文**
    存在无数个，只有在函数被调用时才会被创建，每次调用函数都会创建一个新的执行上下文
- **Eval函数执行上下文**
    指的是运行在eval函数中的代码

执行上下文的生命周期包括：创建阶段、执行阶段、回收阶段

<span style = 'color:red;font-weight:bold;font-size:19px'>执行栈</span>
执行站（调用栈），具有先进后出的结构，用于存储代码执行期间创建的所有执行上下文。
当Javascript引擎开始执行你第一行脚本代码的时候，它就会创建一个全局执行上下文然后将它压到执行栈中

每当引擎碰到一个函数的时候，它就会创建一个函数执行上下文，然后将这个执行上下文压到执行栈中

引擎会执行位于执行栈栈顶的执行上下文(一般是函数执行上下文)，当该函数执行结束后，对应的执行上下文就会被弹出，然后控制流程到达执行栈的下一个执行上下文

---
### 什么是原型以及原型链

<span style = 'color:red;font-weight:bold;'>原型prototype</span>

每个JS对象都有一个内部属性`[[Prototype]]`（可以通过__proto__属性访问），它指向该对象的原型对象。原型对象也是一个普通对象，也有他的原型对象，以此类推，直到最顶层的原型对象`Object.prototype`

<span style = 'color:red;font-weight:bold;'>原型链</span>

当访问一个对象的方法或属性时，首先在该对象本身查找，如果找不到，则会沿着原型链依次向上查找，直到找到该属性/方法，或者到达原型链的顶端（返回一个NULL）

<span style = 'color:red;font-weight:bold;'>作用</span>
**实现代码复用：** 多个对象可以共享原型对象上的属性和方法，避免了代码的重复定义；
**动态性：** 可以在运行时修改原型对象的属性和方法，所有继承自该原型的对象都会受到影响。

**例题一:**

```javaScript
function Foo(){
    getName = function(){ console.log(1) }
    return this
}
Foo.getName = function(){ console.log(2) }
Foo.prototype.getName = function(){ console.log(3) }
var getName = function(){ console.log(4) }
function getName(){
    console.log(5)
}

Foo.getName()   //2
getName()       //4 变量声明优先级>函数声明优先级
Foo().getName() //1
//等同于，Foo()执行
//getName = function(){ console.log(1) }
//return this   即window
getName()      //1
new Foo().getName()   //3
//对象内部没有 --> 构造函数  --> 对象原型__proto__ --> 原型对象prototype
```
**例题二:**
```javaScript
let o = {
      a:10,
      b:{
        fun:function(){
          console.log(this.a)  //undefined
          console.log(this)   //b对象
        }
      }
    }
    o.b.fun()
```   
**例题三：**
```javaScript
window.name = 'hcl'
function A(){
    this.name = 123
}
A.prototype.getA = function(){
    return this.name + 1
}
let a = new A()
let funcA = a.getA
console.log(funcA())  //hcl1
//如果
let funcA = a.getA()
console.log(funcA)  //124
```
**例题四：**
```javaScript
var length = 10
    function fn(){
      return this.length+1
    }
    let obj = {
      length:5,
      test1:function(){
        return fn();
      }
    }
    obj.test2 = fn;
    console.log(obj.test1())  //11 这里直接调用的fn()，因此fn的this指向window。形成了一个闭包
    console.log(fn()===obj.test2())  //false
    console.log(obj.test1()==obj.test2())  //false
```
---
### JS的继承
**1、通过原型链继承**

```javaScript
function Father(){
    this.arr = [1,2,3]
}
function Child(){

}
Child.prototype = new Father()
let o1 = new Child();
let o2 = new Child();
console.log(o1.arr,o2.arr)    //[1,2,3]    [1,2,3]

//缺点：原型中包含的引用之会在所有实例间共享，“牵一发而动全身”
//原因：在使用原型继承时，原型实际上时另一个类型的实例
o1.arr[0]='xxx'
console.log(o1.arr,o2.arr)    //['xxx',2,3]    ['xxx',2,3]
```

**2、借用构造函数继承**

```javaScript
function Father(){
    this.arr = [1,2,3]
}
Father.prototype.name = 'father'
function Child(){
    Father.call(this)
}
let o1 = new Child();
let o2 = new Child();
console.log(o1,arr,o2.arr)    //[1,2,3]    [1,2,3]

//解决了原型链继承问题
o1.arr[0]='xxx'
console.log(o1,arr,o2.arr)    //['xxx',2,3]    [1,2,3]

//但是只能继承父类实例上的方法和属性，无法访问父类原型上的方法或属性
console.log(o1.name,o2.name)   //undefined undefined

```

**3、组合继承**
解决了原型链方法和借用构造函数方法的缺点，但是带来了多构造一次的开销

**4、ES class继承**
```javaScript
class Father{
    constructor(){
        this.arr = [1,2,3]
    }
}
class Chile extends Father{
    constructor(){
        super()
    }  
}

let o1 = new Child();
let o2 = new Child();

console.log(o1,arr,o2.arr)    //[1,2,3]    [1,2,3]
o1.arr[0]='xxx'
console.log(o1,arr,o2.arr)    //['xxx',2,3]    [1,2,3]
```
---
### new关键字做了什么
- 创建了一个空对象
    - const obj = {}
- 让这个空对象的原型（`__proto__`）指向构造函数的prototype
    - `obj.__proto__ = ConstructorFn.prototype`;
    - 这样obj就可以访问到构造函数原型上的属性和方法
- 执行构造函数，this指向这个新对象
    - `ConstructorFn.call(obj)`，如果构造函数内部给this添加属性，这些属性都会加到obj上
- 如果构造函数有返回值且是一个对象，就返回这个对象，否则返回第一步创建的对象

```javaScript
function myNew(constructor,...args){
    const obj = {}
    obj.__proto__ = constructor.prototype
    const result = constructor.apply(obj,args)
    return (typeof result === 'object'&&result!==null)? result:obj
}
```
---
### 函数声明和函数表达式的区别
<span style = 'color:red;font-weight:bold;'>函数声明式</span>
**1、语法结构**
```javaScript
function myFunction(){
    //函数体
}
```
**2、提升**
函数声明会被提升到作用域的顶部，从而可以在函数定义之前使用调用该函数
**3、可命名**
**4、使用场景**——函数声明通常用于定义全局或模块局功能
**5、作用域**——在其所在的作用域内可用


<span style = 'color:red;font-weight:bold;'>函数表达式</span>
**1、语法结构**
```javaScript
const myfunction  = function(){
    //函数体
}
```
**2、没有提升**——只有在执行到定义它的那一行才能调用该函数，提前调用会抛出`TypeError`
函数声明会被提升到作用域的顶部，从而可以在函数定义之前使用调用该函数
**3、可命名也可以匿名**，如果是命名的常用于递归
```javaScript
const myFunction = function namedFunction(){
    nameFunction()   //递归调用
}
```
**4、使用场景**——更常用于回调，闭包，或者在特定场合需要动态创建函数时
**5、作用域**——函数表达式的可用性取决于其定义的时机

---
### call、apply、bind的区别

call、apply和bind的作用使用来改变函数执行时的上下文（即this指向），区别在于传入对的参数和返回值

**1、call方法**
允许调用一个函数，并指定该函数内部的this指向，并且可以传入一个或多个参数
- 语法：
```JavaScript
function.call(thisArg,arg1,arg2,...)
//thisArg为函数执行时this的值，后面的参数时传给函数的参数列表，call方法返回一个立即执行函数
```
**2、apply方法**
允许调用一个函数，并指定该函数内部的this指向，并且可以传入一个或多个参数，参数以数组的形式传递
- 语法：
```JavaScript
function.call(thisArg,[argsArray])
//thisArg为函数执行时this的值，argsArr是一个数组，包含传递给函数的参数，apply方法返回一个立即执行函数
```
**3、bind方法**
允许调用一个函数，并指定该函数内部的this指向，并且可以传入一个或多个参数
- 语法：
```JavaScript
function.bind(thisArg,arg1,arg2,...)
//thisArg为函数执行时this的值，后面的参数时传给函数的参数列表
//bind不会返回一个立即执行函数，而是返回一个新的函数，可以稍后调用该函数
```

---
### 深拷贝与浅拷贝
**浅拷贝**只复制对象或数组的引用，而不是对象或数组的本身。如果原始对象中有引用类型的数据（对象/数组），则浅拷贝后的对象中的引用数据类型仍然是原始对象中的引用，修改拷贝后的数据会对原始数据造成影响。
常见的浅拷贝方法有：Object.assign()，展开运算符，slice()、concat()……

**深拷贝**会递归的赋值所有引用数据类型，包括对象中的对象，数组中的数组，从而生成一个全新的对象/数组，对拷贝后的对象进行修改不会影响到原始对象。
常见的深拷贝方法有：JSON.parse()+JSON.Stringfy()、lodash库、jQuery.extend()、手动递归复制
```javaScript
function deepCopy(obj){
    if(obj===null||typeof obj!=='object')
        return obj
    let copy = Array.isArray(obj)?[]:{}
    for(let key in obj){
        if(obj.hasOwnProperty(key)){
            copy[key] = deepCopy(obj[key])
        }
    }
    return copy
}
```
---
### ES6可选链操作符
可选链操作符是js中的一种语法，允许安全地访问对象内部深层嵌套属性，而不必显示检查每个级别地存在性，语法为`?.`在访问属性式，如果前面地表达式为null，或undefined，则整个表达式的指为undefined，而不是抛出错误
```javaScript
const info = [
      {
        name:'zhangsan',
        age:18,
        address:{
          province:'anhui',
          city:'maanshan'
        }
      },
      {
        name:'wangwu',
        age:28,
      },
      {
        name:'lisi',
        age:20,
        address:{
          province:'jiangsu',
          city:'nanjing'
        }
      }
    ]
    const province = info.map(item=>item.address?.province)
    console.log(province)   //['anhui', undefined, 'jiangsu']
```
---
### 箭头函数与普通函数的区别
比较点 | 普通函数 | 箭头函数
---|---|---|
this 指向 | 动态绑定，调用时决定 | 静态绑定，取决于定义时所在的上下文
arguments 对象 | 有自己的 arguments | 没有自己的 arguments（可以用剩余参数 ...args 代替）
能否作为构造函数 | 可以（可以用 new 调用，生成实例对象） | 不可以（用 new 调用箭头函数会报错）
prototype 属性 | 有 prototype 属性 | 没有 prototype 属性
是否能绑定 this | 可以用 bind、call、apply | bind、call、apply 无法改变箭头函数的 this
语法简洁性 | 普通写法 | 更加简洁，尤其是单行表达式

---
### Promise
#### 如何理解Promise
promise是一个异步编程的解决方案，主要解决的就是没有promise之前的回调函数问题，因为回调函数可能会出现“回调地狱”的现象，使得代码不易阅读，不好维护。
Promise本身是一个对象，`Proimise.then`或`Promise.catch`是微任务，每一个`then`都返回一个Promise，Promise就是一个容器，Promise对象代表一个异步操作，包含三个状态，进行中，已成功，已失败.
每一个then都是一个单独的作用域，在某一个then中定义的变量在其他的then中是无法直接使用的。
Promise还有一些其他的方法，比如all、race，在项目中如果有多个请求，需要一起返回数据可以用all

<span style="color:red;">补充：</span>
Promise是一个构造函数，通过`new Promise()`来创建一个Promise实例，它接受一个执行器函数作为参数，该执行器函数有两个参数`resolve`和`reject`，分别用于将Promise的状态从pending变为fulfilled和rejected，由用户控制

#### 手写promise
```javaScript
    class myPromise{
      constructor(excutor){
        this.state = 'pending'
        this.value = undefined  //存放成功的值
        this.reason = undefined  //存放失败的原因
        this.onFulfilledCallbacks = []  //成功后的所有回调函数
        this.onRejectedCallbacks = []   //失败后的所有回调函数
        const resolve = (value)=>{     
          if(this.state==='pending'){   //如果状态是pending
            this.state = 'fulfilled'    //状态变成fulfilled
            this.value = value          //保存成功值
            this.onFulfilledCallbacks.forEach(fn=>fn(value))   //并执行所有成功回调
          }
        }
        const reject = (reason)=>{     
          if(this.state==='pending'){   //如果状态是pending
            this.state = 'rejected'     //求改状态为rejected
            this.reason = reason        //保存失败原因
            this.onRejectedCallbacks.forEach(fn=>fn(reason))  //执行所有失败回调函数
          }
        }
        excutor(resolve,reject)    //直接调用excutor，传两个参数，有用户自己决定是成功还是失败
      }
      then(onFulfilled,onRejected){
        return new myPromise((resolve,reject)=>{  //返回一个Promise，从而实现链式调用
          const handleFulfilled = ()=>{
            try{
              const result = onFulfilled(this.value)
              resolve(result)
            }catch(error){
              reject(error)
            }
          }
          const handleRejected = ()=>{
            try{
              const result = onRejected(this.reason)
              resolve(result)
            }catch(error){
              reject(error)
            }
          }
          if(this.state==='fulfilled'){   //如果已经是fulfilled，执行成功回调
            handleFulfilled()
          }else if(this.state === 'rejected'){   //如果已经是fulfilled，执行成功回调
            handleRejected()
          }else{   //resolve和rejecte还没触发，将回调保存
            this.onFulfilledCallbacks.push(handleFulfilled)
            this.onRejectedCallbacks.push(handleRejected)
          }
        })
      }
    }
    const p = new myPromise((resolve,reject)=>{
      resolve()
    })
    p.then(()=>{
      console.log(1)
    }).then(()=>{
      console.log(2)
    }).then(()=>{
      console.log(3)
    })
```
#### Promise的链式调用
```javaScript
const promiseChain = new Promise((resolve,reject)=>{
      setTimeout(()=>{
        resolve(1)
      },1000)
    })
    promiseChain.then((result)=>{
      console.log("first then",result)
      return result+1
    }).then((newResult)=>{
      console.log("second then",newResult)
      return newResult*2
    }).then((finalResult)=>{
      console.log('final result',finalResult)
    }).catch((error)=>{
      console.log('Error',error.message)
    })
//console中的结果为：
//     first then 1
//     second then 2
//     final result 4
```

#### Promise错误捕获的方法
方式一：catch
```javaScript
let promise = new Promise((resolve,reject)=>{
    throw new error('An error occured')
})
promise.catch((error)=>{
    console.error('Error Caught:',error)
})
```

方式二：try…catch
```javaScript
async function asyncFUntion(){
    try{
        throw new Error('An error occured')
    }catch(error){
        console.error('Error Caught:',error)
    }
}
asyncFunction()
```

#### Promise中的all和race有什么区别
promise.all：等待所有Promise完成，只有在所有Promise都成功的情况下成功；
Promise.race：返回第一个完成的Promise，无论成功或失败

---
### setTimeout、Promise、async/await的区别
**1、宏任务与微任务**
setTimeout是一个宏任务
Promise是一个对象，其中的then是微任务
async/await是基于Promise的高级语法糖，也是微任务

**2、使用场景**
setTimeout：主要用于定时器执行任务，使用在特定时间点执行的操作
Promise：用于封装异步操作的结果，提供了一种更加灵活的方式来处理异步逻辑和错误处理
async/await：提供了更简洁、更易于理解的异步变成方式，尤其适合处理复杂的异步逻辑，await后面不管是什么，都会阻塞后面代码，跳出执行同步任务

```javascript
async function async1() {
    console.log('async1 start')
    await async2()    //await修饰，后续console.log直接堵塞，放入微任务队列
    //跳出，直接执行后续同步任务
    console.log('async1 end')
}
async function async2() {
    console.log('async2')      //打印
}
console.log('script start')   //第一个同步任务，直接打印
setTimeout(function () {
    console.log('settimeout')   //异步任务，且是宏任务，进入任务队列
})
async1()        //调用，打印async1 start，调用async2
new Promise(function (resolve) {  
    console.log('promise1')
    resolve()
}).then(function () {    //.then进入微任务
    console.log('promise2')
})
console.log('script end')   //同步任务直接打印，所有同步任务都结束，取微任务，再宏任务
//script start --> async1 satrt --> async2 --> promise1 --> 
//script end --> async1 end --> promise2 --> settimeout
```
----

### 什么是js中的包装类型
包装类型是指将基本数据类型（字符串、数字、布尔值）封装为对象的类型，使得基本数据类型可以使用对象的方法和属性。在js中，当对基本数据类型使用对象的方法是，js会自动将基本值转为对应的包装对象，进行操作后再转回基本值，这种机制被称为**自动装箱**

- new String('example')——返回一个字符串对象
- new Number(123)——返回一个数字对象
- new Boolean(true)——返回一个布尔对象

---

### ajax、axios和fetch的区别
<span style = 'color:red;font-weight:bold;'>AJAX</span>
- **定义：** AJAX是一种用于不重新加载整个页面的情况下与服务器通信的技术。依赖于XMLHttpRequest对象向服务器发送异步请求，然后用js来操作DOM页面
- **优点**
    - 可以在老旧的浏览器中支持
    - 提供了较好的自定义功能
- **缺点**
    - 使用较为复杂
    - 不支持Promise绑定
    - 处理响应式的跨域问题相对复杂

<span style = 'color:red;font-weight:bold;'>Axios</span>
- **定义：** Axios是一个基于Promise的HTTP客户端，用户浏览器和Node.js，它封装了XMLHttpRequest，提供更加简单的API
- **优点**
    - 支持Promise，便于链式调用
    - 可以自动转换JSON数据
    - 拥有请求、相应拦截器，方便处理请求
    - 更好的错误处理
    - 更好的易用性和可读性

<span style = 'color:red;font-weight:bold;'>Fetch</span>
- **定义：** Fetch API是一种现代的、基于Promise的浏览器API，用于进行网络请求。是由原生js提供的，不需要额外的库
- **优点**
    - 语法简洁，基于Promise，适合链式调用
    - 提供更强大的功能和灵活性
    - 支持流读取
- **缺点**
    - 不支持IE浏览器
    - 处理错误时需要额外处理，因为他只在网络错误时返回Rejected状态
    - 需要手动转换响应体
---
### ES6中的proxy
proxy适用于“拦截”对某个对象的访问（读取、修改、函数调用等）的一种机制，可以在访问对象的某些行为前后，自定义额外的操作，并且与Object.defineProperty不同，Proxy是整体代理，不需要手动循环所有属性
```javaScript
const proxy = new Proxy(target, handler)
```
`target`：要代理的数据（原始数据）
`handler`：定义拦截的对象，里面是一些方法
方法名 | 作用
---|---|
get | 拦截属性读取
set | 拦截属性赋值
has | 拦截 in 操作符
deleteProperty | 拦截 delete 操作
ownKeys | 拦截 Object.keys() 和 for...in
apply | 拦截函数调用
construct | 拦截 new 实例化对象

**常见场景：**
- Vue3的响应式原理
- 防止对象被篡改
- 数据校验
- 实现默认值
- 虚拟化接口（Mock数据）
- 智能属性访问
---
### ES6中的Decorator
Decorator是一个普通的函数，用于扩展类属性和类方法
**优点：**
- 代码可读性变强，装饰器命名相当于一个注释
- 在不改变原有代码的情况下，对原有功能进行扩展

**用法：**
- 类的装饰
```javascript
@testable
class MyTestableClass {
  // ...
}
function testable(target) {  //target是要传入的类，实现了为类添加属性
  target.isTestable = true;
}
MyTestableClass.isTestable // true

//传递参数则需要在装饰器外部在封装一层函数
function testable(isTestable) {
  return function(target) {
    target.isTestable = isTestable;
  }
}

@testable(true)
class MyTestableClass {}
MyTestableClass.isTestable // true

@testable(false)
class MyClass {}
MyClass.isTestable // false
```
- 类属性的装饰，能够接受三个参数——类的原型对象、需要装饰的属性名、装饰属性名的描述对象
```javaScript
function readonly(target,name,descriptor){
    descriptor.writable = false
    return descriptor
}

class Person{
    @readonly
    name(){return `${this.first} ${this.last}`}
}
//相当于
readonly(Person.prototype, 'name', descriptor);
```
---
### 尾递归
尾递归是指在一个函数中，最后一步是调用自身，并且直接返回这个调用的结果
尾递归理论上可以复用现有的栈帧，**不需要新增新的调用栈，可以节省内存，防止爆栈**
~~js并没有很好的支持尾递归优化~~

```javaScript
function factorial(n) {
  if (n === 1) return 1;
  return n * factorial(n - 1);
}
console.log(factorial(5)); // 120
```
```javaScript
function factorial(n, total = 1) {
  if (n === 1) return total;
  return factorial(n - 1, n * total);
}

console.log(factorial(5)); // 120
```
可见：尾递归的特点是**递归调用的返回值就是函数的返回值**，中间没有其他的计算或处理

---
### 函数式编程
主要的编程范式有：命令式编程、声明式编程、函数式编程

**函数式编程**更加强调程序执行的结果而非执行的过程，倡导利用若干简单的执行单元让计算结果不断渐进，逐层推到复杂的运算，而非设计一个复杂的执行过程

<span style = 'color:red;font-weight:bold;font-size:19px;'>相关概念</span>
- **纯函数**
    “无副作用”的函数，对给定的输入返回相同的输出的函数，要求所有数据都是不可变的，纯函数=无状态+数据不可变
    ```javascript
    let double = value => value * 2
    ```
- **高阶函数**
    接受函数为输入或者输出的函数被称为高阶函数
    ```javascript
    //手写forEach
    const forEach = function(arr,fn){
        for(let i = 0;i<arr.length;i++){
            fn(arr[i])
        }
    }
    let arr = [1,2,3]
    forEach(arr,(item)=>{
        console.log(item)
    })
    ```
- **柯里化**
    柯里化是将一个多参函数转化为一个嵌套的一元函数的过程
    ```js
    //原函数
    let fn = (x,y) => x*y
    //柯里化
    const curry = function(fn){
        return function(x){
            return function(y){
                return fn(x,y)
            }
        }
    }
    ley myfn = curry(fn)
    console.log( myfn(1)(2) )
    ```
- **组合与管道**
    将多个函数组合成一个函数，从而将很多小的函数组合起来完成更加复杂的逻辑
    
<span style = 'color:red;font-weight:bold;font-size:19px;'>优缺点</span>
- 优点
    1. 更好的状态管理：它的宗旨式无状态或者说更少的状态，能够最大化减少未知、优化代码、减少出错的情况
    2. 更简单的复用：固定输入->固定输出，没有其他外部变量，并且无副作用
    3. 更优雅的组合
    4. 隐性好处，减少代码量，提高维护性
- 缺点
    1. 对方法进行的过度包装可能会引起由频繁切换上下文的性能开销
    2. 资源占用，为了实现对象状态的不可变，往往会创建新的对象
    3. 递归陷阱
----

### 函数缓存
实现函数缓存通常依靠闭包、柯里化、高阶函数

---
### js中的精度丢失问题，如果解决？
js中的精度丢失问题主要是源于浮点数的表示方式，它遵循IEEE 754双精度浮点书标准，使用二进制近似表示小数，导致一些十进制树不能被精确表示，从而出现精度误差
```js
console.log(0.1+0.2 === 0.3)   //false
```
**解决方案**
- 使用toFixed()/toPrecision()处理显示精度——返回字符串，不能继续用于数值计算
- 将小数转为整数再转为小数
- 第三方精度库，`decimal.js`、`big.js`
- ---

### 如何判断一个元素是否在可视区域
- **offset、scrollTop**
```js
function inInViewPortOfOne(el){
      //clientHeight：元素内容区域的高度和上下内边距的高度
      const viewPortHeight = window.innerHeight ||
        document.documentElement.clientHeight ||
        document.body.clientHeight
      const offsetTop = el.offsetTop
      const scrollTop = document.documentElement.scrollTop
      const top = offsetTop - scrollTop
      return top <= viewPortHeight
}
```
- **getBoundingClientRect**，返回一个DOMRect对象，拥有left、top、right、bottom、x、y、width、height属性
```js
function isInViewPort(element) {
  const viewWidth = window.innerWidth || document.documentElement.clientWidth;
  const viewHeight = window.innerHeight || document.documentElement.clientHeight;
  const {
    top,
    right,
    bottom,
    left,
  } = element.getBoundingClientRect();

  return (
    top >= 0 &&
    left >= 0 &&
    right <= viewWidth &&
    bottom <= viewHeight
  );
}
```
- **Intersection Observer**
---
### 大文件如何做断点续传
- **分片上传**——将要上传的文件，按照一定的大小，将整个文件分割成多个数据块来进行分片上传，上传完之后在由服务断对所有文件进行会合后整合为原始文件
    - 将需要上传的文件按照一定的分割规则，分割为相同大小的数据块；
    - 初始化为一个分片上传任务，返回本次分片上传唯一标识；
    - 按照一定策略（串行或并行）发送各个分片数据块
    - 发送完成后，服务端根据判断数据上传是否完整，如果完整，将进行数据块合成得到原始文件
- **断点续传**——在下载或上传时，将下载或上传任务人为分成几个部分。每一个部分采用一个线程进行上传或下载，如果碰到网络故障，可以从已经上传或下载的部分开始继续上传下载未完成的部分，而没有必要从头开始上传下载。用户可以节省时间，提高速度
