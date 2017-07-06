## 一、函数参数的默认值

ES6 之前，不能直接为函数的参数指定默认值，只能采用变通的方法：
```javascript
function log(x, y) {
  y = y || 'World';
  console.log(x, y);
}

log('Hello') // Hello World
log('Hello', 'China') // Hello China
log('Hello', '') // Hello World
```
缺点在于，如果参数y赋值了，但是对应的布尔值为false，则该赋值不起作用。就像上面代码的最后一行，参数y等于空字符，结果被改为默认值。

对比，ES6 允许为函数的参数设置默认值，即直接写在参数定义的后面：
```javascript
function log(x, y = 'World') {
  console.log(x, y);
}

log() // undefined world
log('Hello') // Hello World
log('Hello', 'China') // Hello China
log('Hello', '') // Hello
```

再来看另一个例子：
```javascript
function Point(x = 0, y = 0) {
  this.x = x;
  this.y = y;
}

var p = new Point();
p // { x: 0, y: 0 }
```
上面例子可以得出：设置了默认值的参数，是可以省略的，不用去函数体里面查看，有利于将来代码优化，未来即使删掉这个参数，也不会导致以前代码不能运行。

函数参数默认值结合解构赋值结合使用，注意对比上面：
```javascript
function foo({x, y = 5}) {
  console.log(x, y);
}

foo({}) // undefined, 5
foo({x: 1}) // 1, 5
foo({x: 1, y: 2}) // 1, 2
foo() // TypeError: Cannot read property 'x' of undefined
```
上面代码中，**foo() 是会报错**的！


函数参数变量是默认声明的，所以不能用let或const再次在函数体内声明，如下：
```javascript
function foo(x = 5) {
  let x = 1; // error
  const x = 2; // error
}
```
函数参数的默认值，是每次都重新计算的，如下：
```javascript
let x = 99;
function foo(p = x + 1) {
  console.log(p);
}

foo() // 100

x = 100;
foo() // 10
```

**参数默认值的位置**

通常情况下，定义了默认值的参数，应该是函数的尾参数。因为这样比较容易看出来，到底省略了哪些参数。**如果非尾部的参数设置默认值，实际上这个参数是没法省略的**，如下：
```javascript
// 例一
function f(x = 1, y) {
  return [x, y];
}

f() // [1, undefined]
f(2) // [2, undefined])
f(, 1) // 报错
f(undefined, 1) // [1, 1]

// 例二
function f(x, y = 5, z) {
  return [x, y, z];
}

f() // [undefined, 5, undefined]
f(1) // [1, 5, undefined]
f(1, ,2) // 报错
f(1, undefined, 2) // [1, 5, 2]
```
上面代码中，有默认值的参数都不是尾参数。这时，无法只省略该参数，而不省略它后面的参数，除非显式输入undefined。

如果传入null，则没有这个效果，如下：
```javascript
function foo(x = 5, y = 6) {
  console.log(x, y);
}

foo(undefined, null)
// 5 null
```
**函数的length属性**

指定了默认值以后，函数的length属性，将返回没有指定默认值的参数个数。也就是说，指定了默认值后，length属性将失真。同理rest 参数也不会计入length属性，如下：
```javascript
(function (a) {}).length // 1
(function (a = 5) {}).length // 0
(function (a, b, c = 5) {}).length // 2

(function(...args) {}).length // 0
```

## 二、rest 参数

ES6 引入 rest 参数（形式为...变量名），用于获取函数的多余参数，这样就不需要使用arguments对象了。rest 参数搭配的变量是一个数组，该变量将多余的参数放入数组中，如下：
```javascript
function add(...values) {
  let sum = 0;

  for (var val of values) {
    sum += val;
  }

  return sum;
}

add(2, 5, 3) // 10
```
注意，rest 参数之后不能再有其他参数（即只能是最后一个参数），否则会报错，如下：
```javascript
// 报错
function f(a, ...b, c) {
  // ...
}
```

## 三、严格模式



## 四、箭头函数


## 五、绑定 this