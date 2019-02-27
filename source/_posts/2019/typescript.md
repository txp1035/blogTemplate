---
title: 'typescript'
category: 技术
tags: [笔记, 前端]
date: 2019-2-26
updated: 2019-2-26
---

typescript 学习记...

<!-- more -->

# typescript

## 基础类型

通过冒号+类型来定义变量的类型。

```js
let decLiteral: number = 6; //数字类型的列子
```

### 布尔值（boolean）

### 数字（number）

### 字符串（string）

### Array（数组）

有两种定义方式：

`元素类型[]`

```js
let list: number[] = [1, 2, 3];
```

`Array<元素类型>`

```js
let list: Array<number> = [1, 2, 3];
```

### 元组 Tuple

元组类型允许表示一个已知元素数量和类型的数组，各元素的类型不必相同。

```js
let x: [string, number] = ['hello', 10];
```

当访问一个越界的元素，会使用联合类型替代。

```js
let x: [string, number] = ['hello', 10];
x[3] = 'world'; // OK, 字符串可以赋值给(string | number)类型
x[6] = true; // Error, 布尔不是(string | number)类型
```

### 枚举

枚举类型可以为一组数值赋予友好的名字。

```js
enum Color {Red = 1, Green, Blue}
let colorName: string = Color[2];
console.log(colorName);  // 显示'Green'因为上面代码里它的值是2
```

### Any

任何类型。

### Void

没有任何类型。 当一个函数没有返回值时，你通常会见到其返回值类型是 void。

### Null 和 Undefined

默认情况下 null 和 undefined 是所有类型的子类型。

当你指定了--strictNullChecks 标记，null 和 undefined 只能赋值给 void 和它们各自。

### Never

never 类型表示的是那些永不存在的值的类型。

```js
function error(message: string): never {
  throw new Error(message);
} // 返回never的函数必须存在无法达到的终点
function fail() {
  return error('Something failed');
} // 推断的返回值类型为never
function infiniteLoop(): never {
  while (true) {}
} // 返回never的函数必须存在无法达到的终点
```

### Object

object 表示非原始类型，也就是除 number，string，boolean，symbol，null 或 undefined 之外的类型。

### 类型断言

类型断言好比其它语言里的类型转换，但是不进行特殊的数据检查和解构。 它没有运行时的影响，只是在编译阶段起作用。

类型断言有两种形式。
其一是“尖括号”语法

```js
let someValue: any = "this is a string";
let strLength: number = (<string>someValue).length;
```

另一个为 as 语法。

```js
let someValue: any = "this is a string";
let strLength: number = (someValue as string).length;
```

## 接口

TypeScript 的核心原则之一是对值所具有的结构进行类型检查。 它有时被称做“鸭式辨型法”或“结构性子类型化”。 在 TypeScript 里，接口的作用就是为这些类型命名和为你的代码或第三方代码定义契约。

```js
interface LabelledValue {
  label: string;
} //定义
function printLabel(labelledObj: LabelledValue) {
  console.log(labelledObj.label);
} //使用
let myObj = { size: 10, label: 'Size 10 Object' };
printLabel(myObj);
```

### 可选属性

接口里的属性不全都是必需的。有些是只在某些条件下存在，或者根本不存在。

```js
interface SquareConfig {
  color?: string;
  width?: number;
}
```

### 只读属性

一些对象属性只能在对象刚刚创建的时候修改其值。

```js
interface Point {
    readonly x: number;
    readonly y: number;
}
```

### 额外的属性检查

访问 interface 未定义的属性时会报错，有以下三种方法绕过，

方法一：类型断言

```js
interface IFoo {
  label: string;
}
function bar(foo: IFoo) {
  console.log(foo.label);
}
bar({
  label: 'foooo',
  size: 10,
} as IFoo);
```

方法二：在 interface 里定义额外属性

```js
interface IFoo {
  label: string;
  [propName: string]: any;
}
function bar(foo: IFoo) {
  console.log(foo.label);
}
bar({
  label: 'foooo',
  size: 10
});
```

方法三：赋值给另一属性

```js
interface IFoo {
  label: string;
}
function bar(foo: IFoo) {
  console.log(foo.label);
}
const foo = {
  label: 'foooo',
  size: 10
};
bar(foo);
```

### 函数类型

```js
interface SearchFunc {
  (source: string, subString: string): boolean;
}
let mySearch: SearchFunc;
mySearch = function(source: string, subString: string) {
  let result = source.search(subString);
  return result > -1;
};
```

### 可索引的类型

```js
interface StringArray {
  [index: number]: string;
}
let myArray: StringArray;
myArray = ['Bob', 'Fred'];
let myStr: string = myArray[0];
```

TypeScript 支持两种索引签名：字符串和数字。

### 类类型

```js
interface ClockInterface {
  currentTime: Date;
}
class Clock implements ClockInterface {
  currentTime: Date;
  constructor(h: number, m: number) {}
}
```

当你操作类和接口的时候，你要知道类是具有两个类型的：静态部分的类型和实例的类型。

### 继承接口

```js
interface Shape {
    color: string;
}
interface Square extends Shape {
    sideLength: number;
}
let square = <Square>{};
square.color = "blue";
square.sideLength = 10;
```

### 混合类型

一个对象可以同时做为函数和对象使用，并带有额外的属性。

```js
interface Counter {
    (start: number): string;
    interval: number;
    reset(): void;
}
function getCounter(): Counter {
    let counter = <Counter>function (start: number) { };
    counter.interval = 123;
    counter.reset = function () { };
    return counter;
}
let c = getCounter();
c(10);
c.reset();
c.interval = 5.0;
```

### 接口继承类

当接口继承了一个类类型时，它会继承类的成员但不包括其实现。

```js
class Control {
    private state: any;
}
interface SelectableControl extends Control {
    select(): void;
}
class Button extends Control implements SelectableControl {
    select() { }
}
class TextBox extends Control {
    select() { }
}
// 错误：“Image”类型缺少“state”属性。
class Image implements SelectableControl {
    select() { }
}
class Location {

}
```

## 类

传统的 JavaScript 程序使用函数和基于原型的继承来创建可重用的组件，但对于熟悉使用面向对象方式的程序员来讲就有些棘手，因为他们用的是基于类的继承并且对象是由类构建出来的。

```js
class Greeter {
  greeting: string;
  constructor(message: string) {
    this.greeting = message;
  }
  greet() {
    return 'Hello, ' + this.greeting;
  }
}
let greeter = new Greeter('world');
```

### 继承

子类的 constructor 里可以用 `super(参数)` 或 `super.bar(参数)` 来执行父类的 constructor。

### 公共，私有与受保护的修饰符

public：公有，可以在内部、派生类、声明外部访问；

private：私有，可以在内部访问；

protected：保护，可以在内部、派生类访问；

### readonly 修饰符

你可以使用 readonly 关键字将属性设置为只读的。 只读属性必须在声明时或构造函数里被初始化。

```js
class Octopus {
    readonly name: string;
    readonly numberOfLegs: number = 8;
    constructor (theName: string) {
        this.name = theName;
    }
}
let dad = new Octopus("Man with the 8 strong legs");
dad.name = "Man with the 3-piece suit"; // 错误! name 是只读的.
```

### 参数属性

在上面的例子中，我们必须在 Octopus 类里定义一个只读成员 name 和一个参数为 theName 的构造函数，并且立刻将 theName 的值赋给 name，这种情况经常会遇到。 参数属性可以方便地让我们在一个地方定义并初始化一个成员。 下面的例子是对之前 Octopus 类的修改版，使用了参数属性：

```js
class Octopus {
    readonly numberOfLegs: number = 8;
    constructor(readonly name: string) {
    }
}
```

### 静态属性

```js
class Foo {
  static bar: 'world';
  constructor() {
    console.log(Foo.bar);
  }
}
```

### 抽象类

```js
abstract class Animal {
    abstract makeSound(): void;
    move(): void {
        console.log('roaming the earch...');
    }
}
```

## 函数

### 函数类型

```js
function add(x: number, y: number): number {
  return x + y;
}
let myAdd = function(x: number, y: number): number {
  return x + y;
};
```

### 可选参数和默认参数

```js
function buildName(firstName: string, lastName?: string) {
  if (lastName) return firstName + ' ' + lastName;
  else return firstName;
}
function buildName(firstName: string, lastName = 'Smith') {
  return firstName + ' ' + lastName;
}
```

### 剩余参数

```js
function buildName(firstName: string, ...restOfName: string[]) {
  return firstName + ' ' + restOfName.join(' ');
}
```

## 泛型

```js
function identity(arg: number): number {
  return arg;
}
```

## 枚举类型

## 类型推论

## 类型兼容性

## 高级类型

## Symbols

## 迭代器和生成器

## 模块

## 命名空间

## 命名空间和模块

## 模块解析

## 声明合并

## JSX

## 装饰器

## Mixins

## 三斜线指令

## JavaScript 文件类型检查
