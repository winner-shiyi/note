# 函数的扩展

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

log('Hello') // Hello World
log('Hello', 'China') // Hello China
log('Hello', '') // Hello
```



## 二、rest 参数


## 三、严格模式


## 四、箭头函数


## 五、绑定 this