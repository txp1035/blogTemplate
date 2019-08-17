---
title: '探索JavaScript面向对象的程序设计，实现一个ES6类'
category: 技术
tags: [笔记, 前端]
date: 2019-8-11
---

再看《JavaScript 高级程序设计》...

<!-- more -->

## 什么是面向对象的程序设计

面向对象程序设计（英语：Object-oriented programming，缩写：OOP）是种具有对象概念的程序编程典范，同时也是一种程序开发的抽象方针。它可能包含数据、属性、代码与方法。对象则指的是类的实例。关键词：类与对象、封装、继承、多态。

## ES6 中的 Class

特征:静态方法、实例属性的新写法、静态属性、私有方法私有属性、new.target 属性

## 理解对象

ECMAScript 中没有类的概念，因此它的对象也与基于类的语言中的对象有所不同。

对象在 ECMAScript 中有两种属性:数据属性和访问器属性。

数据属性包含一个数据值的位置。在这个位置可以读取和写入值。数据属性特性：

1. Configurable:表示能否通过 delete 删除属性从而重新定义属性，能否修改属性的特性，或者能否把属性修改为访问器属性。像前面例子中那样直接在对象上定义的属性，它们的这个特性默认值为 true。
2. Enumerable:表示能否通过 for-in 循环返回属性。像前面例子中那样直接在对象上定义的属性，它们的这个特性默认值为 true。
3. Writable:表示能否修改属性的值。像前面例子中那样直接在对象上定义的属性，它们的这个特性默认值为 true。
4. Value:包含这个属性的数据值。读取属性值的时候，从这个位置读;写入属性值的时候，把新值保存在这个位置。这个特性的默认值为 undefined。

访问器属性不包含数据值;它们包含一对儿 getter 和 setter 函数(不过，这两个函数都不是必需的)。 在读取访问器属性时，会调用 getter 函数，这个函数负责返回有效的值;在写入访问器属性时，会调用 setter 函数并传入新值，这个函数负责决定如何处理数据。访问器属性特性：

1. Configurable:表示能否通过 delete 删除属性从而重新定义属性，能否修改属性的特 性，或者能否把属性修改为数据属性。对于直接在对象上定义的属性，这个特性的默认值为 true。
2. Enumerable:表示能否通过 for-in 循环返回属性。对于直接在对象上定义的属性，这 5 个特性的默认值为 true。
3. Get:在读取属性时调用的函数。默认值为 undefined。
4. Set:在写入属性时调用的函数。默认值为 undefined。

访问器属性不能直接定义，必须使用 Object.defineProperty()来定义。

Object.defineProperty(对象、属性的名字、一个描述符对象) 方法可以修改对象属性值的特性，例如：

```js
/* 数据属性例子 */
var people = {};
Object.defineProperty(people, 'name', { value: 'shawn' });
console.log(people); //{ name: 'shawn' }

/* 访问器属性例子 */
var book = {
  _year: 2004,
  edition: 1
};
Object.defineProperty(book, 'year', {
  get: function() {
    return this._year;
  },
  set: function(newValue) {
    if (newValue > 2004) {
      this._year = newValue;
      this.edition += newValue - 2004;
    }
  }
});
book.year = 2005;
console.log(book.edition); //2
```

## 创建对象

```js
var Person = {
  name: 'name',
  sayName: function() {
    alert(this.name);
  }
};
```

创建这个对象需要 6 行代码，如果需要创建 100 个对象就需要些 600 行代码。
虽然 Object 构造函数或对象字面量都可以用来创建单个对象，但这些方式有个明显的缺点:使用同一个接口创建很多对象，会产生大量的重复代码。

### 工厂模式

```js
function createPerson(name) {
  var o = new Object();
  o.name = name;
  o.sayName = function() {
    alert(this.name);
  };
  return o;
}
var person = createPerson('name');
```

遇到需要复制粘贴东西，先想到的就是封装，于是有了工厂模式。这样再创建 100 个对象只需要 8+100=108 行代码，比直接创建节省了近 500 行代码量。但是创建的对象和 createPerson 没有关联性。

优点：抽象了创建具体对象的过程,解决了创建多个相似对象的问题。
缺点：没有解决对象识别的问题(即怎样知道一个对象的类型)。

### 构造函数模式

```js
function Person(name) {
  this.name = name;
  this.sayName = function() {
    alert(this.name);
  };
}
var person = new Person('name');
```

通过构造函数来创建实例对象，实例对象的`__proto__`等于构造函数 Person 的原型对象。通过这个方法构造函数和实例产生了关联。具体关联如下图：

![图片](https://github.com/ShawDanon/blog/blob/master/source/img/2019/8-16-1.jpg)

但是每个实例的方法(sayName)做的是同一件事情，只使用构造函数模式，每次在实例对象时都会创建它(sayName)，一个属性等于在堆内存中多占用了资源，如果创建很多实例对象，耗费的资源就更多了。

优点：解决了对象识别的问题。
缺点：每个方法都要在每个实例上重新创建一遍，创建两个完成同样任务的 Function 实例的确没有必要。

### 原型模式

```js
function Person() {}
Person.prototype.name = 'name';
Person.prototype.sayName = function() {
  alert(this.name);
};
var person = new Person();
//缺点示例
Person.prototype.goods = ['mac pro', 'mac mini'];
var person1 = new Person();
person1.goods; //['mac pro', 'mac mini']
var person2 = new Person();
person2.goods.push('phone'); //['mac pro', 'mac mini', 'phone']
person1.goods.push('phone'); //['mac pro', 'mac mini', 'phone']
```

通过上面的关系图可以得知，我们在构造函数的原型上创建值可以共享给构造函数的所有实例（其实就是实例在本身找不到属性的时候会通过`__proto__`向上查找属性，直到查找到`Object.prototype`）。这样就解决了构造函数浪费资源的问题。但是这个模式就不能设置实例属性了，重要的是构造函数的原型属性为引用类型的时候，实例可以对它进行修改。

优点：解决了构造函数的方法重复实例问题。
缺点：1、和构造函数模式相比，省略了初始化参数这一步，这让所有实例默认都为相同的属性值。2、所有值都是共享的，如果原型上的值为引用类型，一个实例修改后其他实例同样会被修改。

### 组合使用构造函数模式和原型模式（常用）

创建自定义类型的最常见方式，就是组合使用构造函数模式与原型模式。

```js
function Person(name) {
  this.name = name;
}
Person.prototype = {
  constructor: Person,
  sayName: function() {
    alert(this.name);
  }
};
var person = new Person('name');
```

优点：构造函数模式用于定义实例属性，而原型模式用于定义方法和共享的属性。结果，每个实例都会有自己的一份实例属性的副本，但同时又共享着对方法的引用，最大限度地节省了内存。另外，这种混成模式还支持向构造函数传递参数;可谓是集两种模式之长。
缺点：有其他 OO（面向对象）语言经验的开发人员在看到独立的构造函数和原型时，很可能会感到非常困惑。

### 动态原型模式

```js
function Person(name) {
  //属性
  this.name = name;
  //方法
  if (typeof this.sayName != 'function') {
    Person.prototype.sayName = function() {
      alert(this.name);
    };
  }
}
var friend = new Person('name');
friend.sayName();
```

只有在第一次创建实例的时候初始化方法。为了更像其他语言的面向对象语法。
优点：所有信息都封装在了构造函数中，而通过在构造函数中初始化原型(仅在必要的情况下)，又保持了同时使用构造函数和原型的优点。

### 寄生构造函数模式

```js
function SpecialArray() {
  //创建数组
  var values = new Array();
  values.push.apply(values, arguments);
  //添加方法
  values.toPipedString = function() {
    return this.join('|');
  };
  //返回数组
  return values;
}
var colors = new SpecialArray('red', 'blue', 'green');
alert(colors.toPipedString()); //"red|blue|green"
```

我们想创建一个具有额外方法的特殊数组。由于不能直接修改 Array 构造函数。

### 稳妥构造函数模式

```js
function Person(name) {
  //创建要返回的对象
  var o = new Object();
  //可以在这里定义私有变量和函数
  var a = '私有变量';
  //添加方法
  o.sayName = function() {
    console.log(a);
    alert(name);
  };
  //返回对象
  return o;
}
var friend = Person('name');
friend.sayName();
```

防止外部访问

## 继承

许多 OO 语言都支持两种继承方式:接口继承和实现继承。接口继承只继承方法签名，而实现继承则继承实际的方法。如前所述，由于函数没有签名， 在 ECMAScript 中无法实现接口继承。ECMAScript 只支持实现继承，而且其实现继承主要是依靠原型链来实现的。

### 原型链

```js
function SuperType() {
  this.name = '父类属性';
}
SuperType.prototype.getSuperValue = function() {
  return this.name;
};
function SubType() {
  this.subname = '子类属性';
}
//继承了 SuperType
SubType.prototype = new SuperType();
var instance = new SubType();
instance.name; //父类属性
```

通过子构造函数的原型指向父构造函数的实例，实现了子构造函数的实例和父构造函数的实例与原型在同一原型链上，这样子构造函数的实例就可以访问父构造的属性（父构造函数的实例访问）和方法（父构造函数的原型上访问）了。

缺点：1、共享父类实例，修改值影响其他子实例。2、在创建子类型的实例时，不能向超类型的构造函数中传递参数。实际上，应该说是没有办法在不影响所有对象实例的情况下，给超类型的构造函数传递参数。

### 借用构造函数

```js
function SuperType(name) {
  this.name = name;
}
function SubType() {
  //继承了 SuperType，同时还传递了参数
  SuperType.call(this, 'Nicholas');
  //实例属性
  this.age = 29;
}
var instance = new SubType();
alert(instance.name); //"Nicholas";
alert(instance.age); //29
```

通过 call 调用父构造函数，将父构造函数的属性赋值给子构造函数的属性实现继承。
优点：可以在子类型构造函数中向超类型构造函数传递参数。
缺点：方法都在构造函数中定义，因此函数复用就无从谈起了。

### 组合继承（常用）

```js
function SuperType(name) {
  this.name = name;
  this.colors = ['red', 'blue', 'green'];
}
SuperType.prototype.sayName = function() {
  alert(this.name);
};
function SubType(name, age) {
  //继承属性
  SuperType.call(this, name); //第二次调用SuperType()
  this.age = age;
}
//继承方法
SubType.prototype = new SuperType(); //第一次调用SuperType()
SubType.prototype.constructor = SubType;
```

结合原型链和借用构造函数模式，由于借用构造函数模式在子构造函数复制了父构造函数属性，所以子构造函数的实例会优先访问自己的属性而不会访问父构造函数实例的属性。缺点是会调用两次父构造函数造成资源浪费。

### 原型式继承

```js
function object(o) {
  function F() {}
  F.prototype = o;
  return new F();
}

var person = {
  name: 'Nicholas',
  friends: ['Shelby', 'Court', 'Van']
};
var anotherPerson = object(person);
```

省掉了原型链继承的父构造函数，直接继承一个实例对象
缺点:属性共享，引用类型值被修改会影响其他对象。

### 寄生式继承

```js
function object(o) {
  function F() {}
  F.prototype = o;
  return new F();
}
function createAnother(original) {
  var clone = object(original); //通过调用函数创建一个新对象
  //以某种方式来增强这个对象
  clone.sayHi = function() {
    alert('hi');
  };
  //返回这个对象
  return clone;
}
```

### 寄生组合式继承（最有效）

所谓寄生组合式继承，即通过借用构造函数来继承属性，通过原型链的混成形式来继承方法。
寄生+借用构造函数模式

```js
function object(o) {
  function F() {}
  F.prototype = o;
  return new F();
}
function inheritPrototype(subType, superType) {
  var prototype = object(superType.prototype);
  prototype.constructor = subType;
  subType.prototype = prototype;
}
```

通过寄生模式让子构造函数的原型指向父构造函数的原型实现方法继承，通过借用构造函数模式在子构造函数实例中实现属性继承。
优点：这个例子的高效率体现在它只调用了一次 SuperType 构造函数，并且因此避免了在 SubType. prototype 上面创建不必要的、多余的属性。

## 参考

《JavaScript 高级程序设计》第六章
[《ECMAScript 6 入门》](http://es6.ruanyifeng.com/#docs/class)
[维基百科](https://zh.wikipedia.org/wiki/面向对象程序设计)
