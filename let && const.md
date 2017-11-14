### let
`let`声明特点:
1. 只在其所属代码块有效  
2. 不存在变量提升
3. 存在`暂时性死区(temporal dead zone)`：禁止未声明提前使用变量
4. 不可重复声明

ES6块级作用域：  
函数声明：ES6 引入了块级作用域，明确允许在块级作用域之中声明函数。ES6 规定，块级作用域之中，函数声明语句的行为类似于`let`，在块级作用域之外不可引用。但是，由于浏览器实现不遵守上面规定，有自己的行为，行为类似于`var`声明的变量。
```js
  // 浏览器的 ES6 环境
  function f() { console.log('I am outside!'); }
  (function () {
    var f = undefined;
    if (false) {
      function f() { console.log('I am inside!'); }
    }

    f();
  }());
  // Uncaught TypeError: f is not a function
```
### const
`const`声明特点：
1. 只读，声明后无法改变
2. 声明时必须初始化，不能留到以后赋值
3. 和`let`声明一样，只在其所属块级作用域有效
4. 存在`暂时性死区`，声明变量不提升
5. 不可重复声明

本质：`const`声明的变量其实是指向的内存地址不允许变动，对于简单的数据类型就是对应的值，但对于复杂数据类型（主要是数据和对象），是该值对应的内存地址。
```js
  const foo = {};

  // 为 foo 添加一个属性，可以成功
  foo.prop = 123;
  foo.prop // 123

  // 将 foo 指向另一个对象，就会报错
  foo = {}; // TypeError: "foo" is read-only
```
### ES6声明变量6中方式
1. let
2. const
3. var
4. function
5. import
6. class

ES6为了改变全局对象问题，一方面规定，为了保持兼容性，var命令和function命令声明的全局变量，依旧是顶层对象的属性；另一方面规定，let命令、const命令、class命令声明的全局变量，不属于顶层对象的属性。也就是说，从 ES6 开始，全局变量将逐步与顶层对象的属性脱钩。
```js
  var a = 1;
  // 如果在 Node 的 REPL 环境，可以写成 global.a
  // 或者采用通用方法，写成 this.a
  window.a // 1

  let b = 1;
  window.b // undefined
```
