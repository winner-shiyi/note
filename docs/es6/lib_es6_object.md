## 一、属性的简洁表示

ES6 允许直接写入变量和函数，作为对象的属性和方法。如下：
```javascript
var foo = 'bar';
var baz = {foo};
baz // {foo: "bar"}

// 等同于
var baz = {foo: foo};
```
说明ES6 允许在对象之中，直接写变量。这时，属性名为变量名, 属性值为变量的值。下面是另一个例子:
```javascript
function f(x, y) {
    return {x, y};
}
// 等同于
function f(x, y) {
    return {x: x, y: y};
}
f(1, 2) // objct {x: 1, y: 2}
```
除了属性简写，方法也可以简写，如下：
```javascript
var birth = '2000/01/01';
var Person = {
    name: '魏娜',
    birth,
    // 等同于hello: function(){}
    hello() {
        console.log(`my info is：${this.name} : ${this.birth}`)
    }
}
Person.hello() // my info is：魏娜 : 2000/01/01
```
属性的赋值器（setter）和取值器（getter），事实上也是采用这种写法，如下：
```javascript
var cart = {
    _wheel: 4,
    get wheel() {
        return this._wheel;
    },
    set wheel(val) {
        if(val < this._wheel) {
            throw new Error('数值太小了！');
        }
        this._wheel = val; 
    }
}
cart.wheel = 1; // 报错 数值太小了！
cart.wheel; // 4
cart.wheel = 5;
cart.wheel; // 5
```

一个例子，对象的属性永远是字符串！！！加深一下理解：
```javascript
var ms = {x: 1, y: 2};
function getItem(key) {
    return key in ms ? ms[key] : null;
}
function setItem(key, val) {
    ms[key] = val;
}
getItem(x) // 报错
getItem("x") // 1
setItem(z, 3) // 报错
setItem("z", 3) // 成功
ms // Object {x: 1, y: 2, z: 3}
```
简洁写法的**属性名总是字符串**，这会导致一些看上去比较奇怪的结果，class是字符串，所以不会因为它属于关键字，而导致语法解析报错，如下：
```javascript
var obj = {
  class () {}
};

// 等同于

var obj = {
  'class': function() {}
};
```

## 二、属性名表达式

如果使用字面量方式定义对象（使用大括号），在 ES5 中只能使用（标识符）定义属性，如下：
```javascript
var obj = {
  foo: true,
  abc: 123
};
```
ES6 允许字面量定义对象时，用（表达式）作为对象的属性名，即把表达式放在方括号内，如下：
```javascript
var lastWord = 'last word';

var a = {
  'first word': 'hello',
  [lastWord]: 'world'
};

a['first word'] // "hello"
a[lastWord] // "world"
a['last word'] // "world"
```
注意，属性名表达式如果是一个对象，默认情况下会自动将对象转为字符串[object Object]，这一点要特别小心，如下：
```javascript
const keyA = {a: 1};
const keyB = {b: 2};

const myObject = {
  [keyA]: 'valueA',
  [keyB]: 'valueB'
};

myObject // Object {[object Object]: "valueB"}
```
上面代码中，[keyA]和[keyB]得到的都是[object Object]，所以[keyB]会把[keyA]覆盖掉，而myObject最后只有一个[object Object]属性。

## 三、方法的name属性
函数的name属性，返回函数名。对象方法也是函数，因此也有name属性，如下：
```javascript
const person = {
  sayName() {
    console.log('hello!');
  },
};

person.sayName.name   // "sayName"
```
## 四、Object.is()

Object.is()就是用来比较两个值是否严格相等，与严格比较运算符（===）的行为基本一致，不同之处只有两个：一是+0不等于-0，二是NaN等于自身。
```javascript
// ===运算符中
+0 === -0 //true
NaN === NaN // false
// Object.is中
Object.is(+0, -0) // false
Object.is(NaN, NaN) // true

Object.is('foo', 'foo')
// true
Object.is({}, {})
// false
```
## 五、Object.assign()对象合并

Object.assign方法用于对象的合并，将源对象（source）的所有可枚举属性，复制到目标对象（target）。第一个参数是目标对象，后面的参数都是源对象。

注意，如果目标对象与源对象有同名属性，或多个源对象有同名属性，则后面的属性会覆盖前面的属性。

```javascript
var target = { a: 1, b: 2};

var source1 = { b: 2, c: 4 };
var source2 = { c: 3 };

Object.assign(target, source1, source2);
target // Object {a: 1, b: 2, c: 3}
```
如果undefined和null不在首参数，就不会报错，如下：
```javascript
let obj = {a: 1};
Object.assign(obj, undefined) === obj // true
Object.assign(obj, null) === obj // true

Object.assign(undefined, obj) //报错
Object.assign(null, obj) //报错
```
其他类型的值（即数值、字符串和布尔值）不在首参数，也不会报错。但是，除了字符串会以数组形式，拷贝入目标对象(因为只有字符串的包装对象，会产生可枚举属性)，其他值都不会产生效果:
```javascript
var v1 = 'abc';
var v2 = true;
var v3 = 10;

var obj = Object.assign({}, v1, v2, v3);
console.log(obj); // { "0": "a", "1": "b", "2": "c" }
```
**注意点：**

1、Object.assign方法实行的是浅拷贝，而不是深拷贝。也就是说，如果源对象某个属性的值是对象，那么目标对象拷贝得到的是这个对象的引用。
```javascript
var obj1 = {a: {b: 1}};
var obj2 = Object.assign({}, obj1);

obj1.a.b = 2;
obj2.a.b // 2
```
上面代码中，源对象obj1的a属性的值是一个对象，Object.assign拷贝得到的这个对象的引用，所以这个对象的任何变化，也都会反映在目标对象上面。

2、Object.assign可以用来处理数组，但是会把数组视为对象：
```javascript
Object.assign([1, 2, 3], [4, 5])
// [4,5,3]
```
### Object.assign的常见用途：

（1）为对象添加属性

通过Object.assign方法，将x属性和y属性添加到Point类的对象实例:
```javascript
class Point {
  constructor(x, y) {
    Object.assign(this, {x, y});
  }
}
```
（2）为对象添加方法

```javascript
Object.assign(SomeClass.prototype, {
  someMethod(arg1, arg2) {
    ···
  },
  anotherMethod() {
    ···
  }
});

// 等同于下面的写法
SomeClass.prototype.someMethod = function (arg1, arg2) {
  ···
};
SomeClass.prototype.anotherMethod = function () {
  ···
};
```
上面代码使用了对象属性的简洁表示法，直接将两个函数放在大括号中，再使用assign方法添加到SomeClass.prototype之中

（3）克隆对象
```javascript
function clone(origin) {
  return Object.assign({}, origin);
}
```
上面代码将原始对象拷贝到一个空对象，就得到了原始对象的克隆。

不过，采用这种方法克隆，**只能克隆原始对象自身的值，不能克隆它继承的值**。如果想要保持继承链，可以采用下面的代码:
```javascript
function clone(origin) {
  let originProto = Object.getPrototypeOf(origin);
  return Object.assign(Object.create(originProto), origin);
}
```
（4）合并多个对象

将多个对象合并到某个目标对象上：
```javascript
const merge = 
    (target, ...sources) => Object.assign(target, ...sources);
```
如果希望合并后返回一个新对象，则可以对一个空对象合并：
```javascript
const merge = 
    (...sources) => Object.assign({}, ...sources);
```
（5）为属性指定默认值
```javascript
const DEFAULTS = {
  logLevel: 0,
  outputFormat: 'html'
};

function processContent(options) {
  options = Object.assign({}, DEFAULTS, options);
  console.log(options);
  // ...
}
```
DEFAULTS对象是默认值，options对象是用户提供的参数。Object.assign方法将DEFAULTS和options合并成一个新对象，如果两者有同名属性，则option的属性值会覆盖DEFAULTS的属性值。

**注意**，由于存在浅拷贝的问题，DEFAULTS对象和options对象的所有属性的值，最好都是简单类型，不要指向另一个对象。否则，DEFAULTS对象的该属性很可能不起作用:
```javascript
const DEFAULTS = {
  url: {
    host: 'example.com',
    port: 7070
  },
};
function processContent(options) {
  options = Object.assign({}, DEFAULTS, options);
  console.log(options);
}
processContent({ url: {port: 8000} })
// { url:{port:8000}
```
本意是想将url.port改成8000，url.host不变。实际结果却是options.url覆盖掉DEFAULTS.url，所以url.host就不存在了。

## 六、属性的遍历

ES6 一共有5种方法可以遍历对象的属性：

1、for...in

for...in循环遍历对象自身的和继承的可枚举属性（不含 Symbol 属性）

2、Object.keys(obj)
Object.keys返回一个数组，包括对象自身的（不含继承的）所有可枚举属性（不含 Symbol 属性）

3、Object.getOwnPropertyNames(obj)

Object.getOwnPropertyNames返回一个数组，包含对象自身的所有属性（不含 Symbol 属性，但是包括不可枚举属性）

4、Object.getOwnPropertySymbols(obj)

Object.getOwnPropertySymbols返回一个数组，包含对象自身的所有 Symbol 属性

5、Reflect.ownKeys(obj)

Reflect.ownKeys返回一个数组，包含对象自身的所有属性，不管属性名是 Symbol 或字符串，也不管是否可枚举

以上的5种方法遍历对象的属性，都遵守同样的**属性遍历的次序规则**：

- 首先遍历所有属性名为数值的属性，按照数字排序。
- 其次遍历所有属性名为字符串的属性，按照生成时间排序。
- 最后遍历所有属性名为 Symbol 值的属性，按照生成时间排序。

```javascript
Reflect.ownKeys({ [Symbol()]:0, b:0, 10:0, 2:0, a:0 })
// ['2', '10', 'b', 'a', Symbol()]
```
Reflect.ownKeys方法返回一个数组，包含了参数对象的所有属性。这个数组的属性次序是这样的：首先是数值属性2和10，其次是字符串属性b和a，最后是 Symbol 属性。






















