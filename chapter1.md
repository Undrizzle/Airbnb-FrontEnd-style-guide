# JavaScript编码规范

## 类型

### 1.1 基本类型：直接存取基本类型。

* 字符串
* 数值
* 布尔类型
* null
* undefined

```js
const foo = 1
let bar = foo

bar = 9

console.log(foo, bar)   // => 1, 9
```

### 1.2 复杂类型：通过引用的方式存取复杂类型。

* 对象
* 数组
* 函数

```js
const foo = [1, 2]
const bar = foo

bar[0] = 9

console.log(foo[0], bar[0])  // => 9, 9
```

## 引用

### 2.1 对所有的引用使用 const ，不要使用 var 。这能确保你无法对引用重新赋值，也不会导致出现 bug 或难以理解。

```js
// bad
var a = 1
var b = 2

// good
const a = 1
const b = 2
```

### 2.2 如果你一定需要可变动的引用，使用 let 代替 var 。因为 let 是块级作用域，而 var 是函数作用域。

```js
// bad
var count = 1
if (true) {
    count += 1
}

// good, use the let
let count = 1
if (true) {
    count += 1
}
```

### 2.3 注意 let 和 const 都是块级作用域。

```js
// const 和 let 只存在于它们被定义的区块内
{
    let a = 1
    const b = 1
}
console.log(a)  // ReferenceError
console.log(b)  // ReferenceError
```

## 对象

### 3.1 使用字面值创建对象。

```js
// bad
cosnt item = new Object()

// good
const item = {}
```

### 3.2 如果你的代码在浏览器环境下执行，别使用保留字作为键值。这样的话在IE8不会运行。但在 ES6 模块和服务器端中使用没有问题。



