# 变量的解构赋值

## 数组的解构赋值

### 基本用法

```javascript
let [a, b, c] = [1, 2, 3];
```
ES6 允许写成上面这样,可以从数组中提取值，按照对应位置，对变量赋值。

本质上，这种写法属于“模式匹配”，只要等号两边的模式相同，左边的变量就会被赋予对应的值。下面是一些使用嵌套数组进行解构的例子：

```javascript
let [foo, [[bar], baz]] = [1, [[2], 3]];
foo // 1
bar // 2
baz // 3

let [ , , third] = ["foo", "bar", "baz"];
third // "baz"

let [x, , y] = [1, 2, 3];
x // 1
y // 3

let [head, ...tail] = [1, 2, 3, 4];
head // 1
tail // 注意是 [2, 3, 4]  

let [x, y, ...z] = ['a'];
x // "a"
y // 注意是 undefined
z // 注意是 []
```
**如果解构不成功，变量的值就等于undefined**。

另一种情况是不完全解构，即等号左边的模式，只匹配一部分的等号右边的数组。这种情况下，解构依然可以成功，如下例子：
```javascript
let [x, y] = [1, 2, 3];
x // 1
y // 2

let [a, [b], d] = [1, [2, 3], 4];
a // 1
b // 2
d // 4
```
如果等号的右边不是数组（或者严格地说，不是可遍历的结构，参见《Iterator》），那么将会报错，如下：
```javascript
// 报错
let [foo] = 1;
let [foo] = false;
let [foo] = NaN;
let [foo] = undefined;
let [foo] = null;
let [foo] = {};
```
上面的语句都会报错，因为等号右边的值，要么转为对象以后不具备 Iterator 接口（前五个表达式），要么本身就不具备 Iterator 接口（最后一个表达式）。

对于 Set 结构，也可以使用数组的解构赋值。
```javascript
let [x, y, z] = new Set(['a', 'b', 'c']);
x // "a"
```
只要某种数据结构具有 Iterator 接口，都可以采用数组形式的解构赋值。fibs是一个 Generator 函数（参见《Generator 函数》），原生具有 Iterator 接口。解构赋值会依次从这个接口获取值。如下：
```javascript 
function* fibs() {
  let a = 0;
  let b = 1;
  while (true) {
    yield a;
    [a, b] = [b, a + b];
  }
}

let [first, second, third, fourth, fifth, sixth] = fibs();
sixth // 5
```
### 默认值

解构赋值允许指定默认值。

```javascript
let [foo = true] = []; // foo = true
let [x, y = 'b'] = ['a']; // x='a', y='b'
let [x, y = 'b'] = ['a', undefined]; // x='a', y='b'
```
第三个表达式，y后面的赋值严格等于undefined，所以默认值会生效，为默认值'b'。

```javascript
let [x = 1] = [undefined];
x // 1

let [x = 1] = [null];
x // null
```
**注意**，ES6 内部使用严格相等运算符（===），判断一个位置是否有值。所以，如果一个数组成员不严格等于undefined，默认值是不会生效的。上面的代码中，第一个表达式中：数组成员x被赋值后为undefined，undefined === undefined，所以默认值生效；
第二个表达式中：如果一个数组成员是null，默认值就不会生效，因为null不严格等于undefined。


如果默认值是一个表达式，那么这个表达式是**惰性求值**的，即只有在用到的时候，才会求值。

```javascript
function f() {
  console.log('aaa');
}

let [x = f()] = [1,2,3];
```
上面代码中，因为x能取到值，所以函数f根本不会执行。上面的代码其实等价于下面的代码。
```javascript
let x;
if ([1,2,3][0] === undefined) {
  x = f();
} else {
  x = [1,2,3][0];
}
```
默认值可以引用解构赋值的其他变量，但**该变量必须已经声明**。
```javascript
let [x = 1, y = x] = [2];    // x=2; y=2
let [x = 1, y = x] = [1, 2]; // x=1; y=2
let [x = 1, y = x] = [];     // x=1; y=1
let [x = y, y = 1] = [];     // ReferenceError
```
第一个个表达式x默认值为1，后被重新赋值为2，因为y是引用x的值。

第二个表达式y默认值为引用x的值1，但后面被重新赋值。

对比看第三个和第四个表达式，第四个之所以会报错，是因为x用到默认值y的时候，y还没有声明。


## 对象的解构赋值

对象的解构与数组有一个重要的不同。数组的元素是按顺序排列的，变量的取值由它的位置顺序决定；而对象的属性没有顺序，变量必须与属性同名，才能取到正确的值。
```javascript
let { bar, foo } = { foo: "aaa", bar: "bbb" };
foo // "aaa"
bar // "bbb"

let { baz } = { foo: "aaa", bar: "bbb" };
baz // undefined
```
第二个表达式的变量没有对应的同名属性，导致取不到值，最后等于undefined。

如果变量名与属性名不一致，必须写成下面这样。
```javascript
var { foo: baz } = { foo: 'aaa', bar: 'bbb' };
baz // "aaa"

let obj = { first: 'hello', last: 'world' };
let { first: f, last: l } = obj;
f // 'hello'
l // 'world
```
对象的解构赋值的内部机制，是先找到同名属性，然后再赋给对应的变量。真正被赋值的是变量，而不是属性。

上面代码中，**foo是匹配的模式，baz才是变量。真正被赋值的是变量baz，而不是模式foo。**

注意，采用上面的写法时，变量的声明和赋值是一体的。对于let和const来说，变量不能重新声明，所以一旦赋值的变量以前声明过，就会报错。
```javascript
let foo;
let {foo} = {foo: 1}; // SyntaxError: Duplicate declaration "foo"

let baz;
let {bar: baz} = {bar: 1}; // SyntaxError: Duplicate declaration "baz"
```
因为解构赋值的变量都会重新声明，所以报错。解决方法就是在 let命令下面的一行使用圆括号包起来，因为解析器会将起首的大括号理解成一个代码块，而不是赋值语句，如下：
```javascript
let foo;
({foo} = {foo: 1}); // 成功

let baz;
({bar: baz} = {bar: 1}); // 成功
```
**注意**：

如果要将一个已经声明的变量用于解构赋值，必须非常小心：
```javascript
// 错误的写法
let x;
{x} = {x: 1};
// SyntaxError: syntax error
```
报错的原因是因为js引擎会将{x}理解成一个代码块，解决方法是使用圆括号包起来，如下：
```javascript
// 正确的写法
let x;
({x} = {x: 1});
```

和数组一样，解构也可以用于嵌套结构的对象。
```javascript
var node = {
  loc: {
    start: {
      line: 1,
      column: 5
    }
  }
};

var { loc: { start: { line }} } = node;
line // 1
loc  // error: loc is undefined
start // error: start is undefined
```
上面代码中，只有line是变量，loc和start都是模式，不会被赋值。

对象的解构也可以指定默认值，如下：
```javascript
var {x = 3} = {};
x // 3

var {x, y = 5} = {x: 1};
x // 1
y // 5

var {x:y = 3} = {};
y // 3

var {x:y = 3} = {x: 5};
y // 5

var { message: msg = 'Something went wrong' } = {};
msg // "Something went wrong"
```
和数组一样，默认值生效的条件是：对象的属性的值严格等于undefined
```javascript
var {x = 3} = {x:undefined};
x // 3

var {x = 3} = {x:null};
x // null
```
undefined就会触发函数参数的默认值，如下：
```javascript
[1, undefined, 3].map((x = 'yes') => x);
// [ 1, 'yes', 3 ]
```

如果解构模式是嵌套的对象，而且子对象所在的父属性不存在，那么将会报错。
```javascript
// 报错
let {foo: {bar}} = {baz: 'baz'};
```
由于数组本质是特殊的对象，因此可以对数组进行对象属性的解构，如下：
```javascript
let arr = [1, 2, 3];
let {0 : first, [arr.length - 1] : last} = arr;
first // 1
last // 3
```
上面代码对数组进行解构，数组arr的0键对应的值是1，[arr.length - 1]就是2键，对应的是3。

## 字符串的解构赋值

字符串也可以解构赋值。这是因为此时，字符串被转换成了一个类似数组的对象，如下：
```javascript
const [a, b, c, d, e] = 'hello';
a // "h"
b // "e"
c // "l"
d // "l"
e // "o"
```

类似数组的对象都有一个length属性，因此还可以对这个属性解构赋值，如下：
```javascript
let {length : len} = 'hello';
len // 5
```

## 数值和布尔值的解构赋值

**解构赋值的规则是，只要等号右边的值不是对象或数组，就先将其转为对象**。由于undefined和null无法转为对象，所以对它们进行解构赋值，都会报错。
```javascript
let { prop: x } = undefined; // TypeError
let { prop: y } = null; // TypeError

let {toString: s} = 123;
s === Number.prototype.toString // true

let {toString: s} = true;
s === Boolean.prototype.toString // true
```
## 函数参数的解构赋值

函数的参数也可以使用解构赋值，如下：
```javascript
[[1, 2], [3, 4]].map(([a, b]) => a + b);
// [ 3, 7 ]
```
函数参数的解构也可以使用默认值，如下：
```javascript
function move({x = 0, y = 0} = {}) {
  return [x, y];
}

move({x: 3, y: 8}); // [3, 8]
move({x: 3}); // [3, 0]
move({}); // [0, 0]
move(); // [0, 0]
```
注意对比，上面的例子中函数move的参数是一个对象，通过对象解构，得到变量x和y的值，可以理解成{x:x=0,y:y=0}这样一个参数形式，指定了变量x和y的默认值。而下面的例子为move函数的参数指定的是x和y，没有为变量x和变量y指定默认值，所以得到不同的结果。
```javascript
function move({x, y} = { x: 0, y: 0 }) {
  return [x, y];
}

move({x: 3, y: 8}); // [3, 8]
move({x: 3}); // [3, undefined]
move({}); // [undefined, undefined]
move(); // [0, 0]
```

## 解构赋值的用途

（1）交换变量的值
```javascript
let x = 1;
let y = 2;

[x, y] = [y, x];
```
（2）从函数返回多个值

函数只能返回一个值，如果要返回多个值，只能将它们放在数组或对象里返回。有了解构赋值，取出这些值就非常方便。
```javascript
// 返回一个数组

function example() {
  return [1, 2, 3];
}
let [a, b, c] = example();

// 返回一个对象

function example() {
  return {
    foo: 1,
    bar: 2
  };
}
let { foo, bar } = example();
```
（3）函数参数的定义

解构赋值可以方便地将一组参数与变量名对应起来。
```javascript
// 参数是一个数组
function f([x, y, z]) { ... }
f([1, 2, 3]);

// 参数是一个对象
function f({x, y, z}) { ... }
f({z: 3, y: 2, x: 1});
```
（4）快速提取JSON数据

解构赋值对提取JSON对象中的数据，尤其有用。
```javascript
let jsonData = {
  id: 42,
  status: "OK",
  data: [867, 5309]
};

let { id, status, data: number } = jsonData;

console.log(id, status, number);
// 42, "OK", [867, 5309]
```
（5）函数参数的默认值
```javascript
jQuery.ajax = function (url, {
  async = true,
  beforeSend = function () {},
  cache = true,
  complete = function () {},
  crossDomain = false,
  global = true,
  // ... more config
}) {
  // ... do stuff
};
```
（6）遍历Map结构

任何部署了Iterator接口的对象，都可以用for...of循环遍历。Map结构原生支持Iterator接口，配合变量的解构赋值，获取键名和键值就非常方便。
```javascript
var map = new Map();
map.set('first', 'hello');
map.set('second', 'world');

for (let [key, value] of map) {
  console.log(key + " is " + value);
}
// first is hello
// second is world
```
（7）输入模块的指定方法

加载模块时，往往需要指定输入哪些方法。解构赋值使得输入语句非常清晰。
```javascript
const { SourceMapConsumer, SourceNode } = require("source-map");
```























