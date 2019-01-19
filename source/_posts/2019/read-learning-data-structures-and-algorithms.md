---
title: '记一次H5开发'
category: 技术
tags: [笔记, 前端]
date: 2018-9-28
updated: 2018-9-28
---

《学习 JavaScript 数据结构与算法》读书笔记

<!-- more -->

# 读书笔记

## 数组

概念：

> 最简单的内存数据结构。

## 栈

### 栈的概念

> 栈是一种遵从后进先出(LIFO)原则的有序集合。
> 新添加的或待删除的元素都保存在栈的末尾，称做栈顶，另一端就叫栈底。
> 在栈里，新元素都靠近栈顶，旧元素都接近栈底。

### 栈的创建

```js
function Stack() {
  var items = [];
  this.push = function(element) {
    items.push(element);
  }; //入栈
  this.pop = function() {
    return items.pop();
  }; //出栈，返回出站元素
  this.peek = function() {
    return items[items.length - 1];
  }; //返回栈顶元素
  this.isEmpty = function() {
    return items.length === 0;
  }; //返回栈是否为空
  this.clears = function() {
    items = [];
  }; //清空栈
  this.sizes = function() {
    return items.length;
  }; //返回栈里元素个数
  this.print = function() {
    console.log(items.toString());
  }; //打印栈
}
```

### 从十进制到二进制

```js
function divideBy2(decNumber) {
  var remStack = new Stack(),
    rem,
    binaryString = '';
  while (decNumber > 0) {
    rem = Math.floor(decNumber % 2);
    remStack.push(rem);
    decNumber = Math.floor(decNumber / 2);
  } //取余数入栈
  while (!remStack.isEmpty()) {
    binaryString += remStack.pop().toString();
  } //出栈获得2进制数
  return binaryString;
} //十进制转二进制
function baseConverter(decNumber, base) {
  var remStack = new Stack(),
    rem,
    baseString = '',
    digits = '0123456789ABCDEF';
  while (decNumber > 0) {
    rem = Math.floor(decNumber % base);
    remStack.push(rem);
    decNumber = Math.floor(decNumber / base);
  }
  while (!remStack.isEmpty()) {
    baseString += digits[remStack.pop()];
  }
  return baseString;
} //十进制转任意进制（最多16进制）
```

其他实例：平衡圆括号和汉诺塔

## 队列

### 队列的概念

> 队列是遵循 FIFO（First In First Out，先进先出，也称为先来先服务）原则的一组有序的项。
> 队列在尾部添加新元素，并从顶部移除元素。
> 最新添加的元素必须排在队列的末尾。

### 创建队列

```js
function Queue() {
  var items = [];
  this.enqueue = function(element) {
    itmes.push(element);
  }; //向队列尾部添加一个（或多个）新的项
  this.dequeue = function() {
    return items.shift();
  }; //移除队列的第一（即排在队列最前面的）项，并返回被移除的元素。
  this.front = function() {
    return items[0];
  }; //返回队列中第一个元素——最先被添加，也将是最先被移除的元素。队列不做任何变动。
  this.isEmpty = function() {
    return items.length === 0;
  }; //如果队列中不包含任何元素，返回true，否则返回false。
  this.sizes = function() {
    return items.length;
  }; //返回队列包含的元素个数，与数组的length属性类似。
  this.print = function() {
    console.log(items.toString());
  };
}
```

### 优先队列

```js
function PriorityQueue() {
  var items = [];
  function QueueElement(element, priority) {
    this.element = element;
    this.priority = priority;
  }
  this.enqueue = function(element, priority) {
    var queueElement = new QueueElement(element, priority);
    if (this.isEmpty()) {
      items.push(queueElement);
    } else {
      var added = false;
      for (var i = 0; i < items.length; i++) {
        if (queueElement.priority < items[i].priority) {
          items.splice(i, 0, queueElement);
          added = true;
          break;
        }
        if (!added) {
          items.push(queueElement);
        }
      }
    }
  };
} //最小优先队列
```

### 循环队列——击鼓传花

```js
function hotPotato(nameList, num) {
  var queue = new Queue();
  for (var i = 0; i < nameList.length; i++) {
    queue.enqueue(nameList[i]);
  }
  var eliminated = '';
  while (queue.size() > 1) {
    for (var i = 0; i < num; i++) {
      queue.enqueue(queue.dequeue());
    }
    eliminated = queue.dequeue();
    console.log(eliminated + '在击鼓传花游戏中被淘汰。');
  }
  return queue.dequeue();
}
```
