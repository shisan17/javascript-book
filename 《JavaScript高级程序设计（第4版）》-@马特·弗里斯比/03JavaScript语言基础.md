# JavaScript 语言基础

## 语法

### 区分大小写

ECMAScript中一切都区分大小写。*无论*是变量、函数名还是操作符，都区分大小写。换句话说，变量test和变量Test是两个不同的变量。

### 标识符

所谓标识符，就是变量、函数、属性或函数参数的名称。

标识符可以由一个或多个下列字符组成：

- 第一个字符必须是一个字母、下划线（_）或美元符号（$）
- 剩下的其他字符可以是字母、下划线、美元符号或数字

ECMAScript标识符使用驼峰大小写形式，即第一个单词的首字母小写，后面每个单词的首字母大写，如：

```javascript
firstSecond
myCar
doSomethingImportant
```

> 【注意】
>
> 关键字、保留字、true、false、null不能作为标识符。

### 注释

ECMAScript采用C语言风格的注释，包括单行注释和多行注释（块注释）。单行注释以两个斜杠字符开头，多行注释以一个斜杠和一个星号（/*）开头，以它们的反向组合（*/）结尾，如：

```javascript
// 单行注释

/* 这是
多行
注释 */
```

### 严格模式

ECMAScript 5增加了严格模式（strict mode）的概念。严格模式是一种不同的JavaScript解析和执行模型，ECMAScript 3的一些不规范写法在这种模式下会被处理，对于不安全的活动将抛出错误。要对整个脚本启用严格模式，在脚本开头加上这一行：

```javascript
"use strict";
```

也可以单独指定一个函数在严格模式下执行，只要把这个预处理指令放到函数体开头即可：

```javascript
function doSomething() {
  "use strict";  // 函数体
}
```

### 语句

ECMAScript中的语句以分号结尾。

省略分号意味着由解析器确定语句在哪里结尾，如下面的例子所示：

```javascript
let sum = a + b      // 没有分号也有效，但不推荐
let diff = a - b;    // 加分号有效，推荐
```

>【注意】
>
>即使语句末尾的分号不是必需的，也应该加上。记着加分号有助于防止省略造成的问题，比如可以避免输入内容不完整。此外，加分号也便于开发者通过删除空行来压缩代码（如果没有结尾的分号，只删除空行，则会导致语法错误）。加分号也有助于在某些情况下提升性能，因为解析器会尝试在合适的位置补上分号以纠正语法错误。

## 关键字和保留字

ECMA-262描述了一组保留的关键字，这些关键字有特殊用途，比如表示控制语句的开始和结束，或者执行特定的操作。按照规定，保留的关键字不能用作标识符或属性名。

```
break       do          in            typeof
case        else        instanceof    varcatch       export      new           voidclass       extends     return        whileconst       finally     super         withcontinue    for         switch        yielddebugger    function    thisdefault     if          throwdelete      import      try
```

规范中也描述了一组未来的保留字，同样不能用作标识符或属性名。虽然保留字在语言中没有特定用途，但它们是保留给将来做关键字用的。

```

始终保留
enum

严格模式下保留：
implements package public interface protected static let private

模块代码中保留：
await
```

## 变量

变量可以用于保存任何类型的数据。

每个变量只不过是一个用于保存任意值的命名占位符。

有3个关键字可以声明变量：var 、 const、 let。

其中，var在ECMAScript的所有版本中都可以使用，而const和let只能在ECMAScript 6及更晚的版本中使用。

### var 关键字

要定义变量，可以使用var操作符（注意var是一个关键字），后跟变量名（即标识符，如前所述）：

```javascript
var message;
```

这行代码定义了一个名为message的变量，可以用它保存任何类型的值。（不初始化的情况下，变量会保存一个特殊值undefined）

ECMAScript实现变量初始化，因此可以同时定义变量并设置它的值：

```javascript
var message = "hello";
```

这里，message被定义为一个保存字符串值hi的变量。像这样初始化变量不会将它标识为字符串类型，只是一个简单的赋值而已。随后，不仅可以改变保存的值，也可以改变值的类型：

```javascript
var message = "hello";
message = 100; // 合法，但是不推荐
```

在这个例子中，变量message首先被定义为一个保存字符串值hello的变量，然后又被重写为保存了数值100。虽然不推荐改变变量保存值的类型，但这在ECMAScript中是完全有效的。但是在TypeScript中则会报错。

#### var 声明作用域

使用var操作符定义的变量会成为包含它的函数的局部变量。比如，使用var在一个函数内部定义一个变量，就意味着该变量将在函数退出时被销毁：

```javascript
function test() {
	var message = "hello"; // 这里在函数内声明了一个局部变量
}

test();
console.log(message); // 出错
```

这里，message变量是在函数内部使用var定义的。函数叫test()，调用它会创建这个变量并给它赋值。调用之后变量随即被销毁，因此示例中的最后一行会导致错误。不过，在函数内定义变量时省略var操作符，可以创建一个全局变量：

```javascript
function test() {
  message = "hi"; // 全局变量
}
test();
console.log(message); // "hi
```

去掉之前的var操作符之后，message就变成了全局变量。只要调用一次函数test()，就会定义这个变量，并且可以在函数外部访问到。

>【注意】
>
>虽然可以通过省略var操作符定义全局变量，但不推荐这么做。在局部作用域中定义的全局变量很难维护，也会造成困惑。这是因为不能一下子断定省略var是不是有意而为之。在严格模式下，如果像这样给未声明的变量赋值，则会导致抛出ReferenceError。

如果需要定义多个变量，可以在一条语句中用逗号分隔每个变量：

```javascript
var message = "hello", // 注意，这里是逗号
isChecked = true,
age = 18;
```

#### var 声明提升（变量提升）

使用var时，下面的代码不会报错。这是因为使用这个关键字声明的变量会自动提升到函数作用域顶部：

```javascript
function foo() {
	console.log(age);
	var age = 18;
}

foo(); // undefined
```

之所以不会报错，是因为ECMAScript在运行时把它看成等价如下代码：

```javascript
function foo() {
	var age;
	console.log(age);
	age = 18;
}

foo(); // undefined
```

这里所谓的“提升”（hoist），也就是把所有变量声明都拉到函数作用域的顶部。



此外，反复多次使用var声明同一个变量也是没有问题的：

```javascript
function foo() {
	var age = 18;
	var age = 28;
	var age = 38;
	console.log(age);
}
foo(); // 38
```

### let 声明

> 【注意】
>
> let 声明的范围是块作用域，而var声明的范围是函数作用域。

```javascript
if(true) {
	var name = 'Mick';
	console.log(name); // Mick
}
console.log(name); // Mick

if(true) {
	let age = 28;
	console.log(age); // 28
}
console.log(age); // ReferenceError: age没有定义
```

在这里，age变量之所以不能在if块外部被引用，是因为它的作用域仅限于该块内部。

块作用域是函数作用域的子集，因此适用于var的作用域限制同样也适用于let。











### const 关键字



### 

 ![image-20210629101112684](https://gitee.com/heyku/picgo/raw/master/20210629101119.png)



## 数据类型

## 操作符

## 语句

## 函数

