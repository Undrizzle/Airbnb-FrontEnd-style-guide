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



