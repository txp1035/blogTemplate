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

> 最简单的内存数据结构。

## 栈

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

## 链表

> 链表存储有序的元素集合,但不同于数组,链表中的元素在内存中并不是连续放置的。
> 每个元素由一个存储元素本身的节点和一个指向下一个元素的引用(也称指针或链接)组成。
> 解决数组起点或中间插入或移除项的成本很高的问题

###　创建一个链表

```js
function LinkedList() {
  var Node = function(element) {
    this.element = element; //添加到列表的值
    this.next = null; //指向列表中下一个节点项的指针
  }; //要加入列表的项
  var length = 0; //列表项的数量
  var head = null; //第一个节点的引用
  this.append = function(element) {
    var node = new Node(element),
      current;
    if (head === null) {
      head = node; //列表中第一个节点
    } else {
      current = head;
      while (current.next) {
        current = current.next;
      } //循环链表,直到找到最后一项
      current.next = node; //找到最后一项,将其next赋为node,建立链接
    }
    length++; //更新列表的长度
  }; //向列表尾部添加一个新的项。
  this.insert = function(position, element) {
    //检查越界值
    if (position >= 0 && position <= length) {
      var node = new Node(element),
        current = head,
        previous,
        index = 0;
      if (position === 0) {
        //在第一个位置添加
        node.next = current;
        head = node;
      } else {
        while (index++ < position) {
          previous = current;
          current = current.next;
        }
        node.next = current;
        previous.next = node;
      }
      length++; //更新列表的长度
      return true;
    } else {
      return false;
    }
  }; //向列表的特定位置插入一个新的项。
  this.removeAt = function(position) {
    //检查越界值
    if (position > -1 && position < length) {
      var current = head,
        previous,
        index = 0;
      if (position === 0) {
        head = current.next; //移除第一项
      } else {
        while (index++ < position) {
          previous = current;
          current = current.next;
        }
        previous.next = current.next; //重点：将previous与current的下一项链接起来:跳过current,从而移除它
      }
      length--;
      return current.element;
    } else {
      return null;
    }
  }; //从列表的特定位置移除一项。
  this.remove = function(element) {
    var current = head,
      previous,
      index = 0;
    while (current) {
      if (element === current.element) {
        if (index === 0) {
          head = current.next; //移除第一项
        } else {
          previous = current;
          current = current.next;
          previous.next = current.next; //重点：将previous与current的下一项链接起来:跳过current,从而移除它
        }
      }
      index++;
    }
  }; //从列表中移除一项。
  this.indexOf = function(element) {
    var current = head,
      index = -1;
    while (current) {
      if (element === current.element) {
        return index;
      }
      index++;
      current = current.next;
    }
    return -1;
  }; //返回元素在列表中的索引。如果列表中没有该元素则返回 -1 。
  this.isEmpty = function() {
    return length === 0;
  }; //如果链表中不包含任何元素,返回 true ,如果链表长度大于0则返回 false 。
  this.size = function() {
    return length;
  }; //返回链表包含的元素个数。与数组的 length 属性类似。
  this.toString = function() {
    var current = head,
      string = '';
    while (current) {
      // string = current.element; //书中写法，这样只能获得最后一项的字符串
      string += current.next ? `${current.element},` : current.element;
      current = current.next;
    }
    return string;
  }; //由于列表项使用了 Node 类,就需要重写继承自JavaScript对象默认的toString 方法,让其只输出元素的值。
  this.print = function() {
    console.log(head);
    console.log(length);
  }; //辅助查看链表
} //单项链表
function DoublyLinkedList() {
  var Node = function(element) {
    this.element = element;
    this.next = null;
    this.prev = null; //新增的
  };
  var length = 0;
  var head = null;
  var tail = null; //新增的
  //这里是方法
  this.insert = function(position, element) {
    //检查越界值
    if (position >= 0 && position <= length) {
      var node = new Node(element),
        current = head,
        previous,
        index = 0;
      if (position === 0) {
        if (!head) {
          head = node;
          tail = node;
        } else {
          node.next = current;
          current.prev = node;
          head = node;
        }
      } else if (position === length) {
        current = tail;
        current.next = node;
        node.prev = current;
        tail = node;
      } else {
        while (index++ < position) {
          previous = current;
          current = current.next;
        }
        node.next = current;
        previous.next = node;
        current.prev = node;
        node.prev = previous;
      }
      length++; //更新列表的长度
      return true;
    } else {
      return false;
    }
  };
  this.removeAt = function(position) {
    //检查越界值
    if (position > -1 && position < length) {
      var current = head,
        previous,
        index = 0;
      //移除第一项
      if (position === 0) {
        head = current.next; // {1}
        //如果只有一项，更新tail //新增的
        if (length === 1) {
          // {2}
          tail = null;
        } else {
          head.prev = null; // {3}
        }
      } else if (position === length - 1) {
        //最后一项 //新增的
        current = tail; // {4}
        tail = current.prev;
        tail.next = null;
      } else {
        while (index++ < position) {
          // {5}
          previous = current;
          current = current.next;
        }
        //将previous与current的下一项链接起来——跳过current
        previous.next = current.next; // {6}
        current.next.prev = previous; //新增的
      }
      length--;
      return current.element;
    } else {
      return null;
    }
  };
} //双向链表
```

## 集合

### 创建一个集合

```js
function Set() {
  var items = {};
  this.add = function(value) {
    if (!this.has(value)) {
      items[value] = value;
      return true;
    }
    return false;
  }; //向集合添加一个新的项。
  this.remove = function(value) {
    if (this.has(value)) {
      delete items[value];
      return true;
    }
    return false;
  }; //从集合移除一个值。
  this.has = function(value) {
    // return value in items; //老办法
    return items.hasOwnProperty(value);
  }; //如果值在集合中，返回true，否则返回false。
  this.clear = function() {
    items = {};
  }; //移除集合中的所有项。
  this.size = function() {
    // var count = 0;
    // for (var prop in items) {
    //   if (items.hasOwnProperty(prop)) {
    //     ++count;
    //   }
    // }
    // return count;
    return Object.keys(items).length;
  }; //返回集合所包含元素的数量。与数组的length属性类似。
  this.values = function() {
    return Object.keys(items);
  }; //返回一个包含集合中所有值的数组。
  this.union = function(otherSet) {
    var unionSet = new Set();
    var values = this.values();
    for (var i = 0; i < values.length; i++) {
      unionSet.add(values[i]);
    }
    values = otherSet.values();
    for (var i = 0; i < values.length; i++) {
      unionSet.add(values[i]);
    }
    return unionSet;
  }; //并集
  this.intersection = function(otherSet) {
    var intersectionSet = new Set();
    var values = this.values();
    for (var i = 0; i < values.length; i++) {
      if (otherSet.has(values[i])) {
        intersectionSet.add(values[i]);
      }
    }
    return intersectionSet;
  }; //交集
  this.difference = function(otherSet) {
    var differenceSet = new Set();
    var values = this.values();
    for (var i = 0; i < values.length; i++) {
      if (!otherSet.has(values[i])) {
        differenceSet.add(values[i]);
      }
    }
    return differenceSet;
  }; //差集
  this.subset = function(otherSet) {
    if (this.size() > otherSet.size()) {
      return false;
    } else {
      var values = this.values();
      for (var i = 0; i < values.length; i++) {
        if (!otherSet.has(values[i])) {
          return false;
        }
      }
      return true;
    }
  };
} //子集
```

## 字典和散列表

### 创建一个字典

```js
function Dictionary() {
  var items = {};
  function set(key, value) {
    items[key] = value;
  } //向字典中添加新元素。
  this.remove = function(key) {
    if (this.has(key)) {
      delete items[key];
      return true;
    }
    return false;
  }; //通过使用键值来从字典中移除键值对应的数据值。
  this.has = function(key) {
    return key in items;
  }; //如果某个键值存在于这个字典中，则返回true，反之则返回false。
  this.get = function(key) {
    return this.has(key) ? items[key] : undefined;
  }; //通过键值查找特定的数值并返回。
  this.clear = function() {}; //将这个字典中的所有元素全部删除。
  this.size = function() {}; //返回字典所包含元素的数量。与数组的length属性类似。
  this.keys = function() {}; //将字典所包含的所有键名以数组形式返回。
  this.values = function() {
    var values = [];
    for (var k in items) {
      if (this.has(k)) {
        values.push(items[k]);
      }
    }
    return values;
  }; //将字典所包含的所有数值以数组形式返回。
}
```
