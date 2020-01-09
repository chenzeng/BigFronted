#Javascript

1. ### 原型与原型链 ### 
    构造函数->prototype->实例原型
    实例-> _proto_ -> 实例原型
    实例原型-> constructor -> 构造函数
    ` Object.prototype.__proto__ === null `
    **原型**：每一个JavaScript对象(null除外)在创建的时候就会与之关联另一个对象，这个对象就是我们所说的原型，每一个对象都会从原型"继承"属性
    **原型链**：由相互关联的原型组成的链状结构就是原型链 （实例->实例原型->对象原型->null）

    [prototype](https://github.com/chenzeng/BigFronted/blob/master/image/prototype.png)

2. ### 作用域 ###
    作用域是指程序源代码中定义变量的区域，函数的作用域基于函数创建的位置

3. ### 闭包 ###
    闭包：能够访问自由变量的函数
    自由变量：是指在函数中使用的，但既不是函数也不是函数的局部变量的变量
    闭包= 函数 + 函数能够访问的变量



### Reference 
[JavaScript深入系列15篇](https://juejin.im/post/59278e312f301e006c2e1510)