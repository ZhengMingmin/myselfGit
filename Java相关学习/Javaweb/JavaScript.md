[快速入门 - 廖雪峰的官方网站 (liaoxuefeng.com)](https://www.liaoxuefeng.com/wiki/1022910821149312/1023020895584256)



## 数据类型和变量

### 数据类型

JavaScript中定义了以下几种数据类型：

#### **Number**

JavaScript不区分整数和浮点数，统一用Number表示，以下都是合法的Number类型：

```javascript
123; // 整数123
0.456; // 浮点数0.456
1.2345e3; // 科学计数法表示1.2345x1000，等同于1234.5
-99; // 负数
NaN; // NaN表示Not a Number，当无法计算结果时用NaN表示
Infinity; // Infinity表示无限大，当数值超过了JavaScript的Number所能表示的最大值时，就表示为Infinity
```



#### **字符串**

字符串是以单引号'或双引号"括起来的任意文本，比如`'abc'`，`"xyz"`等等。

如果字符串内部既包含`'`又包含`"`可以用转义字符`\`来标识。



**转义字符**

转义字符`\`可以转义很多字符，比如`\n`表示换行，`\t`表示制表符，字符`\`本身也要转义，所以`\\`表示的字符就是`\`。



**多行字符串**

```
`这是一个
多行
字符串`;
```



**模板字符串**

要把多个字符串连接起来，可以用`+`号连接：

```
var name = '小明';
var age = 20;
var message = '你好, ' + name + ', 你今年' + age + '岁了!';
alert(message);
```

如果有很多变量需要连接，用`+`号就比较麻烦。ES6新增了一种模板字符串，表示方法和上面的多行字符串一样，但是它会自动替换字符串中的变量：

```
var name = '小明';
var age = 20;
var message = `你好, ${name}, 你今年${age}岁了!`;
alert(message);
```



**操作字符串**

字符串常见的操作如下：

```
var s = 'Hello, world!';
s.length; // 13
```

要获取字符串某个指定位置的字符，使用类似Array的下标操作，索引号从0开始：

```
var s = 'Hello, world!';

s[0]; // 'H'
s[6]; // ' '
s[7]; // 'w'
s[12]; // '!'
s[13]; // undefined 超出范围的索引不会报错，但一律返回undefined
```

*需要特别注意的是*，字符串是不可变的，如果对字符串的某个索引赋值，不会有任何错误，但是，也没有任何效果：

```
var s = 'Test';
s[0] = 'X';
alert(s); // s仍然为'Test'

```



JavaScript为字符串提供了一些常用方法：

1. toUpperCase

`toUpperCase()`把一个字符串全部变为大写：

```
var s = 'Hello';
s.toUpperCase(); // 返回'HELLO'
```

2. toLowerCase

`toLowerCase()`把一个字符串全部变为小写：

```
var s = 'Hello';
var lower = s.toLowerCase(); // 返回'hello'并赋值给变量lower
lower; // 'hello'
```

3. indexOf

`indexOf()`会搜索指定字符串出现的位置：

```
var s = 'hello, world';
s.indexOf('world'); // 返回7
s.indexOf('World'); // 没有找到指定的子串，返回-1
```

4. substring

`substring()`返回指定索引区间的子串：

```
var s = 'hello, world'
s.substring(0, 5); // 从索引0开始到5（不包括5），返回'hello'
s.substring(7); // 从索引7开始到结束，返回'world'
```






#### **布尔值**

布尔值和布尔代数的表示完全一致，一个布尔值只有`true`、`false`两种值，要么是`true`，要么是`false`，可以直接用`true`、`false`表示布尔值，也可以通过布尔运算计算出来。



> `NaN`这个特殊的Number与所有其他值都不相等，包括它自己：
>
> ```js
> NaN === NaN; // false
> ```
>
> 唯一能判断`NaN`的方法是通过`isNaN()`函数：
>
> ```js
> isNaN(NaN); // true
> ```
>
>  
>
> 要特别注意相等运算符`==`。JavaScript在设计时，有两种比较运算符：
>
> 第一种是`==`比较，它会自动转换数据类型再比较，很多时候，会得到非常诡异的结果；
>
> 第二种是`===`比较，它不会自动转换数据类型，如果数据类型不一致，返回`false`，如果一致，再比较。
>
> 由于JavaScript这个设计缺陷，*不要*使用`==`比较，始终坚持使用`===`比较。
>
> ```js
> false == 0; // true
> false === 0; // false
> ```
>
>  
>
> #### null和undefined
>
> `null`表示一个“空”的值，它和`0`以及空字符串`''`不同，`0`是一个数值，`''`表示长度为0的字符串，而`null`表示“空”。
>
> 在其他语言中，也有类似JavaScript的`null`的表示，例如Java也用`null`，Swift用`nil`，Python用`None`表示。但是，在JavaScript中，还有一个和`null`类似的`undefined`，它表示“未定义”。
>
> JavaScript的设计者希望用`null`表示一个空的值，而`undefined`表示值未定义。事实证明，这并没有什么卵用，区分两者的意义不大。大多数情况下，我们都应该用`null`。`undefined`仅仅在判断函数参数是否传递的情况下有用。



#### **数组**

数组是一组按顺序排列的集合，集合的每个值称为元素。JavaScript的数组可以包括任意数据类型。例如：

```
[1, 2, 3.14, 'Hello', null, true];
```

上述数组包含6个元素。数组用`[]`表示，元素之间用`,`分隔。

另一种创建数组的方法是通过`Array()`函数实现：

```
new Array(1, 2, 3); // 创建了数组[1, 2, 3]
```

然而，出于代码的可读性考虑，强烈建议直接使用`[]`。

数组的元素可以通过索引来访问。请注意，索引的起始值为`0`：

```js
var arr = [1, 2, 3.14, 'Hello', null, true];
arr[0]; // 返回索引为0的元素，即1
arr[5]; // 返回索引为5的元素，即true
arr[6]; // 索引超出了范围，返回undefined
```

+ 要取得`Array`的长度，直接访问`length`属性。

+ `Array`可以通过索引把对应的元素修改为新的值

+ 如果通过索引赋值时，索引超过了范围，同样会引起`Array`大小的变化：

  ```js
  var arr = [1, 2, 3];
  arr[5] = 'x';
  arr; // arr变为[1, 2, 3, undefined, undefined, 'x']
  //JavaScript数组越界访问的时候不会报错。
  ```



**array的常用方法：**

**indexOf：**
与String类似，`Array`也可以通过`indexOf()`来搜索一个指定的元素的位置：



**slice**
slice()就是对应String的substring()版本，它截取Array的部分元素，然后返回一个新的Array：

```js
var arr = ['A', 'B', 'C', 'D', 'E', 'F', 'G'];
arr.slice(0, 3); // 从索引0开始，到索引3结束，但不包括索引3: ['A', 'B', 'C']
arr.slice(3); // 从索引3开始到结束: ['D', 'E', 'F', 'G']
```
注意到slice()的起止参数包括开始索引，不包括结束索引。

如果不给slice()传递任何参数，它就会从头到尾截取所有元素。利用这一点，我们可以很容易地复制一个Array：

```js
var arr = ['A', 'B', 'C', 'D', 'E', 'F', 'G'];
var aCopy = arr.slice();
aCopy; // ['A', 'B', 'C', 'D', 'E', 'F', 'G']
aCopy === arr; // false
```



**reverse**

`reverse()`把整个`Array`的元素给调个个，也就是反转：

```
var arr = ['one', 'two', 'three'];
arr.reverse(); 
arr; // ['three', 'two', 'one']
```



**push和pop**

`push()`向`Array`的末尾添加若干元素，`pop()`则把`Array`的最后一个元素删除掉：

```
var arr = [1, 2];
arr.push('A', 'B'); // 返回Array新的长度: 4
arr; // [1, 2, 'A', 'B']
arr.pop(); // pop()返回'B'
arr; // [1, 2, 'A']
arr.pop(); arr.pop(); arr.pop(); // 连续pop 3次
arr; // []
arr.pop(); // 空数组继续pop不会报错，而是返回undefined
arr; // []
```

略

**多维数组**

如果数组的某个元素又是一个`Array`，则可以形成多维数组。







#### **对象**

JavaScript的对象是一组由键-值组成的无序集合，例如：

```
var person = {
    name: 'Bob',
    age: 20,
    tags: ['js', 'web', 'mobile'],
    city: 'Beijing',
    hasCar: true,
    zipcode: null
};
```

JavaScript对象的键都是字符串类型，值可以是任意数据类型。上述`person`对象一共定义了6个键值对，其中每个键又称为对象的属性，例如，`person`的`name`属性为`'Bob'`，`zipcode`属性为`null`。

要获取一个对象的属性，我们用`对象变量.属性名`的方式：

```
person.name; // 'Bob'
person.zipcode; // null
```

+ JavaScript用一个`{...}`表示一个对象，键值对以`xxx: xxx`形式申明，用`,`隔开。注意，最后一个键值对不需要在末尾加`,`，如果加了，有的浏览器（如低版本的IE）将报错。

+ 如果访问一个不存在的属性，JavaScript规定，访问不存在的属性不报错，而是返回`undefined`

+ 由于JavaScript的对象是动态类型，你可以自由地给一个对象添加或删除属性：

```
var xiaoming = {
    name: '小明'
};
xiaoming.age; // undefined
xiaoming.age = 18; // 新增一个age属性
xiaoming.age; // 18
delete xiaoming.age; // 删除age属性
xiaoming.age; // undefined
delete xiaoming['name']; // 删除name属性
xiaoming.name; // undefined
delete xiaoming.school; // 删除一个不存在的school属性也不会报错
```

+ 检测对象是否拥有某一属性，可以用`in`操作符

```js
var xiaoming = {
    name: '小明',
    birth: 1990,
    school: 'No.1 Middle School',
    height: 1.70,
    weight: 65,
    score: null
};
'name' in xiaoming; // true
'grade' in xiaoming; // false
```

但是如果这个属性是该对象继承而来的话那么也不会报错。

要判断一个属性是否是自身拥有的，而不是继承得到的，可以用`hasOwnProperty()`方法：

```js
var xiaoming = {
    name: '小明'
};
xiaoming.hasOwnProperty('name'); // true
xiaoming.hasOwnProperty('toString'); // false
```



> 所有对象最终都会在原型链上指向`object`，所以`xiaoming`也拥有`toString`属性。

### 变量

命名规则：大小写英文字母、数字、下划线和美元符号。且不能用数字开头，不能使用js的关键字。申明一个变量使用var语句。

> 使用 var 申明的变量，作用域是函数体内，存在变量提升现象；
>
> 使用 let 申明的变量，作用域是代码块内，不存在变量提升现象；
>
> 使用 const 申明的是常量，作用域是代码块内，不存在变量提升现象；

**需要注意的是，如果一个变量没有通过var申明就被使用，那么该变量就自动被申明为全局变量**

> 静态语言和动态语言
>
> java是典型的静态语言，静态语言在定义变量时必须指定变量类型，如果赋值的时候类型不匹配，就会报错。
>
> ```js
> int a = 123; // a是整数类型变量，类型用int申明
> a = "ABC"; // 错误：不能把字符串赋给整型变量
> ```
>
>  
>
> js是动态语言，可以把任意数据类型赋值给变量，同一个变量可以反复赋值，而且可以是不同类型的变量，但是要注意只能用`var`申明一次。
>
> ```js
> var a = 123; // a的值是整数123
> a = 'ABC'; // a变为字符串，这个时候不能使用var再次申明a
> ```



**strict模式**

启用方法：在JavaScript代码的第一行写上：

```
'use strict';
```

作用：未经var声明的变量在该模式下，将会导致运行错误。

### 常量

使用const来定义常量

```
const PI = 3.14;
```



### 循环

##### for循环

`for`循环的3个条件都是可以省略的，如果没有退出循环的判断条件，就必须使用`break`语句退出循环，否则就是死循环：

```js
var x = 0;
for (;;) { // 将无限循环下去
    if (x > 100) {
        break; // 通过if判断来退出循环
    }
    x ++;
}
```

**for ... in**

`for`循环的一个变体是`for ... in`循环，它可以把一个对象的所有属性依次循环出来：

```
var o = {
    name: 'Jack',
    age: 20,
    city: 'Beijing'
};
for (var key in o) {
    console.log(key); // 'name', 'age', 'city'
}
```

要过滤掉对象继承的属性，用`hasOwnProperty()`来实现：

```
var o = {
    name: 'Jack',
    age: 20,
    city: 'Beijing'
};
for (var key in o) {
    if (o.hasOwnProperty(key)) {
        console.log(key); // 'name', 'age', 'city'
    }
}
```

由于`Array`也是对象，而它的每个元素的索引被视为对象的属性，因此，`for ... in`循环可以直接循环出`Array`的索引：

```
var a = ['A', 'B', 'C'];
for (var i in a) {
    console.log(i); // '0', '1', '2'
    console.log(a[i]); // 'A', 'B', 'C'
}
```

*请注意*，`for ... in`对`Array`的循环得到的是`String`而不是`Number`。





### Map和Set

#### Map

`Map`是一组键值对的结构，具有极快的查找速度。

初始化`Map`需要一个二维数组，或者直接初始化一个空`Map`。`Map`具有以下方法：

```js
var m = new Map(); // 空Map
m.set('Adam', 67); // 添加新的key-value
m.set('Bob', 59);
m.has('Adam'); // 是否存在key 'Adam': true
m.get('Adam'); // 67
m.delete('Adam'); // 删除key 'Adam'
m.get('Adam'); // undefined
```

#### Set

`Set`和`Map`类似，也是一组key的集合，但不存储value。由于key不能重复，所以，在`Set`中，没有重复的key。重复的元素会被自动过滤。



### iterable

遍历`Array`可以采用下标循环，遍历`Map`和`Set`就无法使用下标。为了统一集合类型，ES6标准引入了新的`iterable`类型，`Array`、`Map`和`Set`都属于`iterable`类型。

一个`Array`数组实际上也是一个对象，它的每个元素的索引被视为一个属性。

例如：

```js
var a = ['A', 'B', 'C'];
a.name = 'Hello';
for (var x in a) {
    console.log(x); // '0', '1', '2', 'name'
}
```

name作为a的属性值的下标索引。



##### forEach

`iterable`内置的`forEach`方法，它接收一个函数，每次迭代就自动回调该函数。以`Array`为例：

```js
'use strict';
var a = ['A', 'B', 'C'];
a.forEach(function (element, index, array) {
    // element: 指向当前元素的值
    // index: 指向当前索引
    // array: 指向Array对象本身
    console.log(element + ', index = ' + index);
});
```

`Set`与`Array`类似，但`Set`没有索引，因此回调函数的前两个参数都是元素本身：

```
var s = new Set(['A', 'B', 'C']);
s.forEach(function (element, sameElement, set) {
    console.log(element);
});
```

`Map`的回调函数参数依次为`value`、`key`和`map`本身：

```
var m = new Map([[1, 'x'], [2, 'y'], [3, 'z']]);
m.forEach(function (value, key, map) {
    console.log(value);
});
```

如果对某些参数不感兴趣，由于JavaScript的函数调用不要求参数必须一致，因此可以忽略它们。例如，只需要获得`Array`的`element`：

```js
var a = ['A', 'B', 'C'];
a.forEach(function (element) {
    console.log(element);
});
```



## 函数

### 函数定义和调用

#### 定义函数

```
function 函数名(参数类型){
	//函数体
}
```

请注意，函数体内部的语句在执行时，一旦执行到`return`时，函数就执行完毕，并将结果返回。

如果没有`return`语句，函数执行完毕后也会返回结果，只是结果为`undefined`。

由于JavaScript的函数也是一个对象，上述定义的`函数名()`函数实际上是一个函数对象，而函数名可以视为指向该函数的变量。



**匿名函数**

```js
var abs = function (x) {
    if (x >= 0) {
        return x;
    } else {
        return -x;
    }
};
```

`function (x) { ... }`是一个匿名函数，它没有函数名。但是，这个匿名函数赋值给了变量`abs`，所以，通过变量`abs`就可以调用该函数。

上述两种定义*完全等价*，注意第二种方式按照完整语法需要在函数体末尾加一个`;`，表示赋值语句结束。

#### 调用函数

调用函数时，按顺序传入参数即可；即使传入的参数比定义的参数多或少也没有问题。传入的多会按顺序匹配，传入的少会返回NaN。

**arguments**

只在函数内部起作用，并且永远指向当前函数的调用者传入的所有参数。

利用`arguments`，你可以获得调用者传入的所有参数。也就是说，即使函数不定义任何参数，还是可以拿到参数的值：

**rest参数**

ES6标准引入了rest参数：

```js
function foo(a, b, ...rest) {
    console.log('a = ' + a);
    console.log('b = ' + b);
    console.log(rest);
}

foo(1, 2, 3, 4, 5);
// 结果:
// a = 1
// b = 2
// Array [ 3, 4, 5 ]

foo(1);
// 结果:
// a = 1
// b = undefined
// Array []
```

rest参数只能写在最后，前面用`...`标识，从运行结果可知，传入的参数先绑定`a`、`b`，多余的参数以数组形式交给变量`rest`，所以，不再需要`arguments`我们就获取了全部参数。

如果传入的参数连正常定义的参数都没填满，也不要紧，rest参数会接收一个空数组（注意不是`undefined`）。



**return**

JavaScript引擎有一个在行末自动添加分号的机制,如果把一个return语句拆成两行的话，就会在return自动加上；

```js
function foo() {
    return; // 自动添加了分号，相当于return undefined;
        { name: 'foo' }; // 这行语句已经没法执行到了
}
```



### 变量作用域与解构赋值

#### 作用域

在JavaScript中，用`var`申明的变量实际上是有作用域的。

如果一个变量在函数体内部申明，则该变量的作用域为整个函数体，在函数体外不可引用该变量。

JavaScript的函数可以嵌套，此时，内部函数可以访问外部函数定义的变量，反过来则不行。

如果内部函数和外部函数的变量名重名，则内部函数的变量将“屏蔽”外部函数的变量。因为JavaScript的函数在查找变量时从自身函数定义开始，从“内”向“外”查找。

##### 全局作用域

不在任何函数内定义的变量就具有全局作用域。

JavaScript默认有一个全局对象，**全局作用域的变量实际上被绑定到的一个属性**：`window`

```js
var course='Learn JavaScript';
alert(course); // 'Learn JavaScript'
alert(window.course); // 'Learn JavaScript'
```

因此，直接访问全局变量`course`和访问`window.course`是完全一样的。

##### 局部作用域

 由于JavaScript的变量作用域实际上是函数内部，我们在循环等语句块中是无法定义具有局部作用域的变量的

为了解决块级作用域，用`let`替代`var`可以申明一个块级作用域的变量。



#### 变量提升

JavaScript的函数定义有个特点，它会先扫描整个函数体的语句，把所有申明的变量“提升”到函数顶部。

```js
'use strict';

function foo() {
    var x = 'Hello, ' + y;
    console.log(x);
    var y = 'Bob';
}

foo();
```

对于上述函数，JavaScript引擎看到的代码相当于：`foo()`

```js
function foo() {
    var y; // 提升变量y的申明，此时y为undefined
    var x = 'Hello, ' + y;
    console.log(x);
    y = 'Bob';
}
```

ps:

由于JavaScript的这一怪异的“特性”，我们在函数内部定义变量时，请严格遵守“在函数内部首先申明所有变量”这一规则。最常见的做法是用一个申明函数内部用到的所有变量：`var`。

#### 解构赋值

在ES6中，可以使用解构赋值，直接对多个变量同时赋值：

```js
var [x, y, z] = ['hello', 'JavaScript', 'ES6'];
//对数组元素进行结构赋值时，多个变量要用[]括起来；

// x, y, z分别被赋值为数组对应元素:
console.log('x = ' + x + ', y = ' + y + ', z = ' + z);

//如果数组本身还有嵌套，注意嵌套层次和位置要保持一致;
let [x, [y, z]] = ['hello', ['JavaScript', 'ES6']];
x; // 'hello'
y; // 'JavaScript'
z; // 'ES6'

//解构赋值还可以忽略某些元素：
let [, , z] = ['hello', 'JavaScript', 'ES6']; // 忽略前两个元素，只对z赋值第三个元素
z; // 'ES6'


//如果需要从一个对象中取出若干属性，也可以使用解构赋值，便于快速获取对象的指定属性：
var person = {
    name: '小明',
    age: 20,
    gender: 'male',
    passport: 'G-12345678',
    school: 'No.4 middle school'
};
var {name, age, passport} = person;
// name, age, passport分别被赋值为对应属性:
console.log('name = ' + name + ', age = ' + age + ', passport = ' + passport);
//name = 小明, age = 20, passport = G-12345678
```





### 方法





