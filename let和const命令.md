## let和const命令

### let (var)

let 声明变量 只在let命令所在的代码块内有效
var 存在变量提升现象 let不存在

如果区块中存在let和const命令，
这个区块对这些命令声明的变量，
从一开始就形成了封闭作用域。
凡是在声明之前就使用这些变量，就会报错。
使用let命令声明变量之前，该变量都是不可用的。这在语法上，称为“暂时性死区”（temporal dead zone，简称 TDZ）
let 不允许在相同作用域内 重复声明同一个变量

### const

const 声明一个只读变量，一旦声明，常量的值就不能改变。

改变常量的值会报错 TypeError

const作用域与let命令相同：只在声明所在的块级作用域内有效

声明的常量不提升，存在暂时性死区，只能在声明的位置后面使用。

const声明的变量也与let一样不可重复声明。

const本质上保证的，不是变量的值不得变动，而是变量指向的那个内存地址所保存的数据不得改动。

对于简单类型的数据（数值、字符串、布尔值），值就保存在变量指向的那个内存地址，因此等同于常量。

但对于复合类型的数据（只要是对象和数组），变量指向的内存地址，保存的只是一个指向实际数据的指针

const只能保证指针是固定的，无法控制其指向的数据结构是否可变。

将对象冻结，应使用object.freeze方法



### ES6声明变量时的六种方法

var，function（from ES5）

let，const，import，class

### 顶层对象的属性

顶层对象，浏览器中指 window 对象，在node中指 global 对象。

ES5中，顶层对象属性与全局变量是等价的。

ES6中，为了保持兼容性，var和function命令声明的全局变量，依旧是顶层对象的属性；

另一方面规定，let、const、class，命令声明的全局变量，不属于顶层对象的属性。

从ES6开始，全局变量将逐步与顶层对象的属性脱钩。

```javascript
var a = 1;
// 如果在 Node 的 REPL 环境，可以写成 global.a
// 或者采用通用方法，写成 this.a
window.a // 1

let b = 1;
window.b // undefined
```

### globalThis对象

浏览器中，顶层对象是window，Node和Web Worker没有window；

浏览器和Web Worker中，self也指向顶层对象，但是Node没有self；

Node 中，顶层对象是global，但其他环境不支持。

全局环境，this 返回顶层对象；

Node和ES6模块中，this返回的是当前模块。

函数中的this，如果函数不是作为对象的方法运行，而是单纯地作为函数运行，this 会指向顶层对象，严格模式下，this会返回undefined。

new Function （‘ return this ’）（），总是返回全局对象，如果浏览器使用了CSP（Content Security Policy，内容安全策略，则eval、new Function这些方法可能都无法使用。

引入globalThis作为顶层对象，则在任何环境下，globalThis都是存在的，都可以从它拿到顶层对象，指向全局环境下的this。
