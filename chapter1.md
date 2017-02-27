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
const item = new Object()

// good
const item = {}
```

### 3.2 如果你的代码在浏览器环境下执行，别使用保留字作为键值。这样的话在IE8不会运行。但在 ES6 模块和服务器端中使用没有问题。

```js
// bad
const superman = {
    default: { clark: 'kent' },
    private: true,
}

// good
const superman = {
    defaults: { clark: 'kent' },
    hidden: true,
}
```

### 3.3 使用同义词替换需要使用的保留字。

```js
// bad
const superman = {
    class: 'alien',
}

// bad
const superman = {
    klass: 'alien',
}

// good
const superman = {
    type: 'alien',
}
```

### 3.4 创建有动态属性名的对象时，使用可被计算的属性名称。因为这样可以让你在一个地方定义所有的对象属性。

```js
function  getKey(k) {
    return `a key named ${k}`
}

// bad
const obj = {
    id: 5,
    name: 'San Francisco',
}
obj[getKey('enabled')] = true

// good
const obj = {
    id: 5,
    name: 'San Francisco',
    [getKey('enabled')]: true,
}
```

### 3.5 使用对象方法的简写。

```js
// bad
const atom = {
    value: 1,

    addValue: function (value) {
        return atom.value + value
    }
}

// good
const atom = {
    value: 1,

    addValue(value) {
        return atom.value + value
    }
}
```

### 3.6 使用对象属性值的简写。因为这样更短更有描述性。

```js
const lukeSkywalker = 'Luke Skywalker'

// bad
const obj = {
    lukeSkywalker: lukeSkywalker,
}

// good
const obj = {
    lukeSkywalker,
}
```

### 3.7 在对象属性声明前把简写的属性分组。因为这样能清楚地看出哪些属性使用了简写。

```js
const anakinSkywalker = 'Anakin Skywalker'
const lukeSkywalker = 'Luke Skywalker'

// bad
const obj = {
    episodeOne: 1,
    twoJedisWalkIntoACantina: 2,
    lukeSkywalker,
    episodeThree: 3,
    mayTheFourth: 4,
    anakinSkywalker,
}

// good
const obj = {
    lukeSkywalker,
    anakinSkywalker,
    episodeOne: 1,
    twoJedisWalkIntoACantina: 2,
    episodeThree: 3,
    mayTheFourth: 4,
}
```

## 数组

### 4.1 使用字面值创建数组。

```js
// bad
const items = new Array()

// good
const items = []
```

### 4.2 向数组添加元素时使用 Array\#push 替代直接赋值。

```js
const someStack = []

// bad
someStack[someStack.length] = 'abracadabra'

// good
someStack.push('abracadabra')
```

### 4.3 使用拓展运算符 ... 赋值数组。

```js
// bad
const len = items.length
const itemCopy = []
let i

for (i = 0; i < len; i++) {
    itemCopy[i] = items[i]
}

// good
const itemsCopy = [...itmes]
```

### 4.4 使用 Array\#from 把一个类数组对象转换成数组。

```js
const foo = document.querySelectorAll('.foo')
const nodes = Array.from(foo)
```

## 解构

### 5.1 使用解构存取和使用多属性对象。因为解构能减少临时引用属性。

```js
// bad
function getFullName(user) {
    const firstName = user.firstName
    const lastName = user.lastName

    return `${firstName} ${lastName}`
}

// good
function getFullName(obj) {
    cosnt { firstName, lastName } = obj
    return `${firstName} ${lastName}`
}

// best
function getFullName({ firstName, lastName }) {
    return `${firstName} ${lastName}`
}
```

### 5.2 对数组使用解构赋值。

```js
const arr = [1, 2, 3, 4]

// bad
const first = arr[0]
const second = arr[1]

// good
const [first, second] = arr
```

### 5.3 需要回传多个值时，使用对象解构，而不是数组解构。增加属性或者改变排序不会改变调用时的位置。

```js
// bad
function processInput(input) {
    // then a miracle occurs
    return [left, right, top, bottom]
}

// 调用时需要考虑回调数据的顺序
const [left, _, top] = processsInput(input)

// good
function processInput(input) {
    // then a miracle occurs
    return { left, right, top, bottom }
}

// 调用时只选择需要的数据
const { left, right } = processInput(input字符串
```

## 字符串

### 6.1 字符串使用单引号 ' ' 。

```js
// bad
const name = "Capt. Janeway"

// good
const name = 'Capt. Janeway'
```

### 6.2 字符串超过80个字节应该使用字符串连接符号换行。

### 6.3 过度使用字符串连接符号可能会对性能造成影响。

```js
// bad
const errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.'

// bad
const errorMessage = 'This is a super long error that was thrown because \
of Batman. When you stop to think about how Batman had anything to do \
with this, you would get nowhere \
fast.'

// good
const errorMessage = 'This is a super long error that was thrown because ' +
  'of Batman. When you stop to think about how Batman had anything to do ' +
  'with this, you would get nowhere fast.'
```

### 6.4 程序化生成字符串时， 使用模板字符串代替字符串连接。因为模板字符串更为简洁，更具可读性。

```js
// bad
function sayHi(name) {
    return 'How are you, ' + name + '?'
}

// bad
function sayHi(name) {
    return ['How are you, ', name, '?'].join()
}

// good
function sayHi(name) {
    return `How are you, ${name}?`
}
```

## 函数

### 7.1 使用函数声明代替函数表达式。因为函数声明是可命名的，所以他们在调用栈中更容易被识别。此外，函数声明会把整个函数提升（hoisted），而函数表达式只会把函数的引用变量名提升。这条规则使得箭头函数可以取代函数表达式。

```js
// bad
const foo = function () {
}

// good
function foo() {
}
```

### 7.2 函数表达式。

```js
// 立即调用的函数表达式（IIFE）
(() => {
    console.log('Welcome to the Internet. Please follow me.')
})()
```

### 7.3 永远不要在一个非函数代码块（if、while等）中声明一个函数，把那个函数赋给一个变量。浏览器允许你这么做，但它们的解析表现不一致。

### 7.4 ECMA-262把 block定义为一组语句。函数声明不是语句。

```js
// bad
if (currentUser) {
    function test() {
        console.log('Nope.')
    }
}

// good
let test
if (currentUser) {
    test = () => {
        console.log('Yup.')
    }
}
```

### 7.5 永远不要把参数命名为 arguments 。这将取代原来函数作用域内的 arguments 对象。

```js
// bad
function nope(name, options, arguments) {
    // ...stuff...
}

// good
function yup(name, options, args) {
    // ...stuff...
}
```

### 7.6 不要使用 arguments ，可以选择 rest 语法 ... 替代。因为使用 ... 能明确你要传入的参数。另外 rest参数是一个真正的数组，而 arguments 是一个类数组。

```js
// bad
funciton concatenateAll() {
    const args = Array.prototype.slice.call(arguments)
    return args.join('')
}


// good
function concatenateAll(...args) {
    return args.join('')
}
```

### 7.7 直接给函数的参数指定默认值，不要使用一个变化的函数参数。

```js
// really bad
function handleThings(opts) {
    // 不！我们不应该改变函数参数
    // 更加糟糕：如果参数 opts 是 false 的话，它就会被设定为一个对象
    // 但这样的写法会造成一些 Bugs
    // 例如当 opts 被赋值为空字符串，opts 仍然会被下一行代码设定为一个空对象
    opts = opts || {}
    // ...
}

// still bad
function handleThings(opts) {
    if (opts === void 0) {
        opts = {}
    }
    // ...
}

// good
function handleThings(opts = {}) {
    // ...
}
```



