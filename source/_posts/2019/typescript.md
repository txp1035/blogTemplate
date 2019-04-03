---
title: 'typescript'
category: 技术
tags: [笔记, 前端]
date: 2019-2-26
---

typescript 学习记...

<!-- more -->

# typescript

## 基础类型

通过冒号+类型来定义变量的类型。

```ts
let decLiteral: number = 6; //数字类型的列子
```

### 布尔值（boolean）

### 数字（number）

### 字符串（string）

### Array（数组）

有两种定义方式：

`元素类型[]`

```ts
let list: number[] = [1, 2, 3];
```

`Array<元素类型>`

```ts
let list: Array<number> = [1, 2, 3];
```

### 元组 Tuple

元组类型允许表示一个已知元素数量和类型的数组，各元素的类型不必相同。

```ts
let x: [string, number] = ['hello', 10];
```

当访问一个越界的元素，会使用联合类型替代。

```ts
let x: [string, number] = ['hello', 10];
x[3] = 'world'; // OK, 字符串可以赋值给(string | number)类型
x[6] = true; // Error, 布尔不是(string | number)类型
```

### 枚举

枚举类型可以为一组数值赋予友好的名字。

```ts
enum Color {
  Red = 1,
  Green,
  Blue
}
let colorName: string = Color[2];
console.log(colorName); // 显示'Green'因为上面代码里它的值是2
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

```ts
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

```ts
let someValue: any = 'this is a string';
let strLength: number = (<string>someValue).length;
```

另一个为 as 语法。

```ts
let someValue: any = 'this is a string';
let strLength: number = (someValue as string).length;
```

## 接口

TypeScript 的核心原则之一是对值所具有的结构进行类型检查。 它有时被称做“鸭式辨型法”或“结构性子类型化”。 在 TypeScript 里，接口的作用就是为这些类型命名和为你的代码或第三方代码定义契约。

```ts
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

```ts
interface SquareConfig {
  color?: string;
  width?: number;
}
```

### 只读属性

一些对象属性只能在对象刚刚创建的时候修改其值。

```ts
interface Point {
  readonly x: number;
  readonly y: number;
}
```

### 额外的属性检查

访问 interface 未定义的属性时会报错，有以下三种方法绕过，

方法一：类型断言

```ts
interface IFoo {
  label: string;
}
function bar(foo: IFoo) {
  console.log(foo.label);
}
bar({
  label: 'foooo',
  size: 10
} as IFoo);
```

方法二：在 interface 里定义额外属性

```ts
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

```ts
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

```ts
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

```ts
interface StringArray {
  [index: number]: string;
}
let myArray: StringArray;
myArray = ['Bob', 'Fred'];
let myStr: string = myArray[0];
```

TypeScript 支持两种索引签名：字符串和数字。

### 类类型

```ts
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

```ts
interface Shape {
  color: string;
}
interface Square extends Shape {
  sideLength: number;
}
let square = <Square>{};
square.color = 'blue';
square.sideLength = 10;
```

### 混合类型

一个对象可以同时做为函数和对象使用，并带有额外的属性。

```ts
interface Counter {
  (start: number): string;
  interval: number;
  reset(): void;
}
function getCounter(): Counter {
  let counter = <Counter>function(start: number) {};
  counter.interval = 123;
  counter.reset = function() {};
  return counter;
}
let c = getCounter();
c(10);
c.reset();
c.interval = 5.0;
```

### 接口继承类

当接口继承了一个类类型时，它会继承类的成员但不包括其实现。

```ts
class Control {
  private state: any;
}
interface SelectableControl extends Control {
  select(): void;
}
class Button extends Control implements SelectableControl {
  select() {}
}
class TextBox extends Control {
  select() {}
}
// 错误：“Image”类型缺少“state”属性。
class Image implements SelectableControl {
  select() {}
}
class Location {}
```

## 类

传统的 JavaScript 程序使用函数和基于原型的继承来创建可重用的组件，但对于熟悉使用面向对象方式的程序员来讲就有些棘手，因为他们用的是基于类的继承并且对象是由类构建出来的。

```ts
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

```ts
class Octopus {
  readonly name: string;
  readonly numberOfLegs: number = 8;
  constructor(theName: string) {
    this.name = theName;
  }
}
let dad = new Octopus('Man with the 8 strong legs');
dad.name = 'Man with the 3-piece suit'; // 错误! name 是只读的.
```

### 参数属性

在上面的例子中，我们必须在 Octopus 类里定义一个只读成员 name 和一个参数为 theName 的构造函数，并且立刻将 theName 的值赋给 name，这种情况经常会遇到。 参数属性可以方便地让我们在一个地方定义并初始化一个成员。 下面的例子是对之前 Octopus 类的修改版，使用了参数属性：

```ts
class Octopus {
  readonly numberOfLegs: number = 8;
  constructor(readonly name: string) {}
}
```

### 静态属性

```ts
class Foo {
  static bar: 'world';
  constructor() {
    console.log(Foo.bar);
  }
}
```

### 抽象类

```ts
abstract class Animal {
  abstract makeSound(): void;
  move(): void {
    console.log('roaming the earch...');
  }
}
```

## 函数

### 函数类型

```ts
function add(x: number, y: number): number {
  return x + y;
}
let myAdd = function(x: number, y: number): number {
  return x + y;
};
```

### 可选参数和默认参数

```ts
function buildName(firstName: string, lastName?: string) {
  if (lastName) return firstName + ' ' + lastName;
  else return firstName;
}
function buildName(firstName: string, lastName = 'Smith') {
  return firstName + ' ' + lastName;
}
```

### 剩余参数

```ts
function buildName(firstName: string, ...restOfName: string[]) {
  return firstName + ' ' + restOfName.join(' ');
}
```

## 泛型

软件工程中，我们不仅要创建一致的定义良好的 API，同时也要考虑可重用性。 组件不仅能够支持当前的数据类型，同时也能支持未来的数据类型，这在创建大型系统时为你提供了十分灵活的功能。

返回值的类型与传入参数的类型是相同的。

```ts
function identity<T>(arg: T): T {
  return arg;
} //定义
let output = identity<string>('myString'); // 使用
let output = identity('myString'); // 普遍使用
```

### 使用泛型变量

我们把泛型变量 T 当做类型的一部分使用，而不是整个类型，增加了灵活性。

```ts
function loggingIdentity<T>(arg: T[]): T[] {
  console.log(arg.length); // Array has a .length, so no more error
  return arg;
}
function loggingIdentity<T>(arg: Array<T>): Array<T> {
  console.log(arg.length); // Array has a .length, so no more error
  return arg;
}
```

### 泛型类

```ts
class GenericNumber<T> {
  zeroValue: T;
  add: (x: T, y: T) => T;
}
let myGenericNumber = new GenericNumber<number>();
myGenericNumber.zeroValue = 0;
myGenericNumber.add = function(x, y) {
  return x + y;
};
```

### 泛型约束

我们需要传入符合约束类型的值，必须包含必须的属性.

```ts
interface Lengthwise {
  length: number;
}
function loggingIdentity<T extends Lengthwise>(arg: T): T {
  console.log(arg.length); // Now we know it has a .length property, so no more error
  return arg;
}
loggingIdentity(3); // Error, number doesn't have a .length property
loggingIdentity({ length: 10, value: 3 });
```

## 枚举类型

使用枚举我们可以定义一些带名字的常量。 使用枚举可以清晰地表达意图或创建一组有区别的用例。

### 数字枚举

```ts
enum Direction {
  Up = 1, //初始化器
  Down,
  Left,
  Right
} //不使用初始化器从0开始
```

### 字符串枚举

在一个字符串枚举里，每个成员都必须用字符串字面量，或另外一个字符串枚举成员进行初始化。

```ts
enum Direction {
  Up = 'UP',
  Down = 'DOWN',
  Left = 'LEFT',
  Right = 'RIGHT'
}
```

### 异构枚举

从技术的角度来说，枚举可以混合字符串和数字成员，但不推荐。

```js
enum BooleanLikeHeterogeneousEnum {
    No = 0,
    Yes = "YES",
}
```

## 类型推论

### 最佳通用类型

当需要从几个表达式中推断类型时候，会使用这些表达式的类型来推断出一个最合适的通用类型。

```ts
let x = [0, 1, null];
```

如果没有找到最佳通用类型的话，类型推断的结果为联合数组类型

### 上下文类型

TypeScript 类型推论也可能按照相反的方向进行。 这被叫做“按上下文归类”。按上下文归类会发生在表达式的类型与所处的位置相关时。

## Symbols

symbol 类型的值是通过 Symbol 构造函数创建的。

```ts
let sym1 = Symbol();
let sym2 = Symbol('key'); // 可选的字符串key
```

Symbols 是不可改变且唯一的。

```ts
let sym2 = Symbol('key');
let sym3 = Symbol('key');
sym2 === sym3; // false, symbols是唯一的
```

像字符串一样，symbols 也可以被用做对象属性的键。

```ts
let sym = Symbol();
let obj = {
  [sym]: 'value'
};
console.log(obj[sym]); // "value"
```

Symbols 也可以与计算出的属性名声明相结合来声明对象的属性和类成员。

```ts
const getClassNameSymbol = Symbol();
class C {
  [getClassNameSymbol]() {
    return 'C';
  }
}
let c = new C();
let className = c[getClassNameSymbol](); // "C"
```

## 模块

模块是自声明的；两个模块之间的关系是通过在文件级别上使用 imports 和 exports 建立的。

### 导出

任何声明（比如变量，函数，类，类型别名或接口）都能够通过添加 export 关键字来导出。

```ts
export { a }; //导出
export { a as b }; //导出重命名
```

一个模块可以包裹多个模块，并把他们导出的内容联合在一起通过语法：`export \* from "module"`。

### 导入

模块的导入操作与导出一样简单。 可以使用以下 import 形式之一来导入其它模块中的导出内容。

```ts
import { ZipCodeValidator } from './ZipCodeValidator'; //导入某个内容
import { ZipCodeValidator as ZCV } from './ZipCodeValidator'; //导入内容重命名
import * as validator from './ZipCodeValidator'; //将整个模块导入到一个变量，并通过它来访问模块的导出部分
```

### 默认导出

每个模块都可以有一个 default 导出。

```ts
declare let $: JQuery;
export default $;

import $ from 'JQuery';
$('button.continue').html('Next Step...');
```

## 命名空间

这篇文章描述了如何在 TypeScript 里使用命名空间（之前叫做“内部模块”）来组织你的代码。 就像我们在术语说明里提到的那样，“内部模块”现在叫做“命名空间”。

```ts
namespace Foo {
  export function bar() {
    console.log(1);
  }
}
Foo.bar();
```

### 别名

另一种简化命名空间操作的方法是使用 import q = x.y.z 给常用的对象起一个短的名字。

```ts
namespace Shapes {
  export namespace Polygons {
    export class Triangle {}
    export class Square {}
  }
}
import polygons = Shapes.Polygons;
let sq = new polygons.Square(); // Same as "new Shapes.Polygons.Square()"
```

### 使用其它的 JavaScript 库

```ts
declare namespace D3 {
  export interface Selectors {
    select: {
      (selector: string): Selection;
      (element: EventTarget): Selection;
    };
  }
  export interface Event {
    x: number;
    y: number;
  }
  export interface Base extends Selectors {
    event: Event;
  }
}
declare var d3: D3.Base;
```

## 命名空间和模块

### 使用命名空间

命名空间是位于全局命名空间下的一个普通的带有名字的 JavaScript 对象。

### 使用模块

像命名空间一样，模块可以包含代码和声明。 不同的是模块可以 声明它的依赖。

### 陷阱

不要用`/// <reference />` 引模块，而是去引 d.ts 文件。

尽量别用命名空间。
