

## CSS

#### 盒模型

box-sizing

- W3C标准盒模型（content-box）element.width = content

- IE盒模型（border-box）element.width = content+padding+border

#### BFC
**块级格式化上下文**（BoxFormattingContext）是一个独立的渲染区域，让处于 BFC 内部的元素与外部的元素相互隔离，使内外元素的定位不会相互影响

- 如何生成(触发条件):

  - 根元素
  - `position: absolute/fixed`
  - `display: inline-block / table/flex`
  - `float` 元素
  - `ovevflow` !== `visible`

- 规则:

  - 属于同一个 BFC 的两个相邻 Box 垂直排列
  - 属于同一个 BFC 的两个相邻 Box 的 margin 会发生重叠
  - BFC 中子元素的 margin box 的左边， 与包含块 (BFC) border box的左边相接触 (子元素 absolute 除外)
  - BFC 的区域不会与 float 的元素区域重叠
  - 计算 BFC 的高度时，浮动子元素也参与计算
  - 文字层不会被浮动层覆盖，环绕于周围

- 应用场景:

  1. 阻止`margin`重叠（加一个div防止在同一个BFC下）
  2. 清除内部浮动(浮动元素参与计算高度，清除浮动的原理是两个`div`都位于同一个 BFC 区域之中) 
  3. 自适应两栏布局（设置overflow:hidden）
  4. 可以阻止元素被浮动元素覆盖

#### 居中布局

  水平居中

  - 行内元素: `text-align: center`
  - 块级元素: `margin: 0 auto`
  - `flex + justify-content: center`
  - `absolute + transform`

  垂直居中

  - `line-height: height`
  - `flex + align-items: center`
  - `table`
  - `absolute + transform`

  水平垂直居中

  - `absolute + transform`
  - `flex + justify-content + align-items`

#### 浮动（TB）

- 父级设置高度
- 创建父级BFC
- 通过增加尾元素清除浮动
  

## JS基础篇

#### 数据类型

最新的 ECMAScript 标准定义了 8种数据类型:

- 基本类型
  Boolean, Null, Undefined, Number,  String
- 引用数据类型
  Object(Date,Array,Function)
- Symbol (ES6新增，这种类型的对象永不相等，即始创建的时候传入相同的值，可以解决属性名冲突的问题，做为标记)
- bigInt (谷歌67版本中还出现了一种 bigInt。是指安全存储、操作大整数)
判断 Target 的类型，单单用 typeof 并无法完全满足，这其实并不是 bug，本质原因是 JS 的万物皆对象的理论。因此要真正完美判断时，我们需要区分对待:

**判断类型**

- 基本类型(null): 使用 String(null)
- 基本类型(string / number / boolean / undefined) + function: 直接使用 typeof即可
- 其余引用类型(Array / Date / RegExp Error): 调用toString后根据[object XXX]进行判断




#### 原型到原型链

**原型**：每一个JavaScript对象(null除外)在创建的时候就会与之关联另一个对象，这个对象就是我们所说的原型，每一个对象都会从原型"继承"属性     

**原型链**：由相互关联的原型组成的链状结构就是原型链 

```
实例.__proto__ === 原型 

原型.constructor === 构造函数

构造函数.prototype === 原型
```

[JavaScript深入之从原型到原型链](https://github.com/mqyqingfeng/Blog/issues/2)

#### 闭包（UClear）

一种特殊的作用域(静态作用域)， 可以理解为**父函数被销毁** 的情况下，返回出的子函数的`[[scope]]`中仍然保留着父级的单变量对象和作用域链，因此可以继续访问到父级的变量对象，这样的函数称为闭包。

闭包会产生一个很经典的问题:

- 多个子函数的`[[scope]]`都是同时指向父级，是完全共享的。因此当父级的变量对象被修改时，所有子函数都受到影响。

解决:

- 变量可以通过 **函数参数的形式** 传入，避免使用默认的`[[scope]]`向上查找
- 使用`setTimeout`包裹，通过第三个参数传入
- 使用 **块级作用域**，让变量成为自己上下文的属性，避免共享

#### this的使用

**this**：(在调用阶段进行绑定，在函数体内部获取当前的运行环境) 是执行上下文创建时确定的一个执行过程中不可更改的变量

- 在全局环境或是普通函数中直接调用
- 作为对象的方法
- 使用apply和call
  - `call: fn.call(target, 1, 2)`
  - `apply: fn.apply(target, [1, 2])`
  - `bind: fn.bind(target)(1,2)`
- 作为构造函数

#### 对象的拷贝

**浅拷贝**: 以赋值的形式拷贝引用对象，仍指向同一个地址，**修改时原对象也会受到影响**

- `Object.assign`
- 展开运算符(...)

**深拷贝**: 完全拷贝一个新对象，**修改时原对象不再受到任何影响**

- ```
  JSON.parse(JSON.stringify(obj)): 性能最快
  ```

  - 具有循环引用的对象时，报错
  - 当值为函数、`undefined`、或`symbol`时，无法拷贝

- 递归进行逐一赋值

#### 防抖与节流

​	**防抖 (debounce)**: 将多次高频操作优化为只在最后一次执行，通常使用的场景是：用户输入，只需再输入完成后做一次输入校验即可

​	**节流(throttle)**: 每隔一段时间后执行一次，也就是降低频率，将高频操作优化成低频操作，通常使用场景: 滚动条事件 或者 resize 事件，通常每隔 100~500 ms执行一次即可

#### ES6新语法

- 声明

  `let / const`: 块级作用域、不存在变量提升、暂时性死区、不允许重复声明

  `const`: 声明常量，无法修改

- 解构赋值

  `class / extend`: 类声明与继承

  `Set / Map`: 新的数据结构

- 异步解决方案:

  `Promise`的使用与实现

  `generator`:

  - `yield`: 暂停代码
  - `next()`: 继续执行代码
  - `await / async`: 是`generator`的语法糖， babel中是基于`promise`实现。

#### 数组(array)

- `map`: 遍历数组，返回回调返回值组成的新数组
- `forEach`: 无法`break`，可以用`try/catch`中`throw new Error`来停止
- `filter`: 过滤
- `some`: 有一项返回`true`，则整体为`true`
- `every`: 有一项返回`false`，则整体为`false`
- `join`: 通过指定连接符生成字符串
- `push / pop`: 末尾推入和弹出，改变原数组， 返回推入/弹出项
- `unshift / shift`: 头部推入和弹出，改变原数组，返回操作项
- `sort(fn) / reverse`: 排序与反转，改变原数组
- `concat`: 连接数组，不影响原数组， 浅拷贝
- `slice(start, end)`: 返回截断后的新数组，不改变原数组
- `splice(start, number, value...)`: 返回删除元素组成的数组，value 为插入项，改变原数组
- `indexOf / lastIndexOf(value, fromIndex)`: 查找数组项，返回对应的下标
- `reduce / reduceRight(fn(prev, cur)， defaultPrev)`: 两两执行，prev 为上次化简函数的`return`值，cur 为当前值(从第二项开始)

