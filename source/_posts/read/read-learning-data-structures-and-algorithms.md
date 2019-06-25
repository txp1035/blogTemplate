---
title: '《学习 JavaScript 数据结构与算法》读书笔记'
category: 兴趣
tags: [阅读笔记]
date: 2019-1-17
---

看完 react 的 diff 算法和 swagger 的数据结构，想温习波数据结构和算法。

<!-- more -->

# 读书笔记 2019-1-17

## 数组

> 最简单的内存数据结构。

## 栈

> 一种顺序数据结构
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

> 一种顺序数据结构
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

### 创建一个链表

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

> 一种非顺序数据结构
> 集合是由一组无序且唯一（即不能重复）的项组成的。
> 集合中的对象列表用`{}`（大括号）包围。

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

### 字典

> 一种非顺序数据结构
> 在字典中，存储的是`[键，值]`对，其中键名是用来查询特定元素的。
> 字典和集合很相似，集合以`[值，值]`的形式存储元素，字典则是以`[键，值]`的形式来存储元素。
> 字典也称作映射。

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

## 散列表

> 一种非顺序数据结构
> 散列表就是通过散列算法将字典的键转化成对应下标值取得键对应的值。
> 散列算法的作用是尽可能快地在数据结构中找到一个值。

### 创建一个散列表

```js
function HashTable() {
  var table = [];
  var loseloseHashCode = function(key) {
    var hash = 0;
    for (var i = 0; i < key.length; i++) {
      hash += key.charCodeAt(i);
    }
    return hash % 37;
  }; //散列函数
  this.put = function(key, value) {
    var position = loseloseHashCode(key);
    console.log(position + ' - ' + key);
    table[position] = value;
  }; //向散列表增加一个新的项(也能更新散列表)
  this.remove = function(key) {
    table[loseloseHashCode(key)] = undefined;
  }; //根据键值从散列表中移除值。
  this.get = function(key) {
    return table[loseloseHashCode(key)];
  }; //返回根据键值检索到的特定的值。
} //带冲突的散列表
function HashTable１() {
  var table = [];
  var loseloseHashCode = function(key) {
    var hash = 0;
    for (var i = 0; i < key.length; i++) {
      hash += key.charCodeAt(i);
    }
    return hash % 37;
  }; //散列函数
  var ValuePair = function(key, value) {
    this.key = key;
    this.value = value;
    this.toString = function() {
      return '[' + this.key + ' - ' + this.value + ']';
    };
  };
  this.put = function(key, value) {
    var position = loseloseHashCode(key);
    if (table[position] == undefined) {
      table[position] = new LinkedList(); //前面的链表
    }
    table[position].append(new ValuePair(key, value));
  }; //向散列表增加一个新的项(也能更新散列表)
  this.remove = function(key) {
    var position = loseloseHashCode(key);
    if (table[position] !== undefined) {
      var current = table[position].getHead();
      while (current.next) {
        if (current.element.key === key) {
          table[position].remove(current.element);
          if (table[position].isEmpty()) {
            table[position] = undefined;
          }
          return true;
        }
        current = current.next;
      }
      // 检查是否为第一个或最后一个元素
      if (current.element.key === key) {
        table[position].remove(current.element);
        if (table[position].isEmpty()) {
          table[position] = undefined;
        }
        return true;
      }
    }
    return false;
  }; //根据键值从散列表中移除值。
  this.get = function(key) {
    var position = loseloseHashCode(key);
    if (table[position] !== undefined) {
      var current = table[position].getHead();
      while (current.next) {
        if (current.element.key === key) {
          return current.element.value;
        }
        current = current.next;
      }
      //检查元素在链表第一个或最后一个节点的情况
      if (current.element.key === key) {
        return current.element.value;
      }
    }
    return undefined;
  }; //返回根据键值检索到的特定的值。
} //分离链接解决散列表冲突
function HashTable２() {
  var table = [];
  var loseloseHashCode = function(key) {
    var hash = 0;
    for (var i = 0; i < key.length; i++) {
      hash += key.charCodeAt(i);
    }
    return hash % 37;
  }; //散列函数
  this.put = function(key, value) {
    var position = loseloseHashCode(key);
    if (table[position] == undefined) {
      table[position] = new ValuePair(key, value);
    } else {
      var index = ++position;
      while (table[index] != undefined) {
        index++;
      }
      table[index] = new ValuePair(key, value);
    }
  }; //向散列表增加一个新的项(也能更新散列表)
  this.remove = function(key) {
    var position = loseloseHashCode(key);
    if (table[position] !== undefined) {
      if (table[position].key === key) {
        return table[position].value;
      } else {
        var index = ++position;
        while (table[index] === undefined || table[index].key !== key) {
          index++;
        }
        table[index] = undefined;
      }
    }
    return undefined;
  }; //根据键值从散列表中移除值。
  this.get = function(key) {
    var position = loseloseHashCode(key);
    if (table[position] !== undefined) {
      if (table[position].key === key) {
        return table[position].value;
      } else {
        var index = ++position;
        while (table[index] === undefined || table[index].key !== key) {
          index++;
        }
        if (table[index].key === key) {
          return table[index].value;
        }
      }
    }
    return undefined;
  }; //返回根据键值检索到的特定的值。
} //线性探查解决散列表冲突
var djb2HashCode = function(key) {
  var hash = 5381;
  for (var i = 0; i < key.length; i++) {
    hash = hash * 33 + key.charCodeAt(i);
  }
  return hash % 1013;
}; //更好的散列函数
```

## 树

> 一种非顺序数据结构
> 它对于存储需要快速查找的数据非常有用。

### 创建 BinarySearchTree 类

```js
function BinarySearchTree() {
  var Node = function(key) {
    this.key = key;
    this.left = null;
    this.right = null;
  };
  var root = null;
  var insertNode = function(node, newNode) {
    if (newNode.key < node.key) {
      if (node.left === null) {
        node.left = newNode;
      } else {
        insertNode(node.left, newNode);
      }
    } else {
      if (node.right === null) {
        node.right = newNode;
      } else {
        insertNode(node.right, newNode);
      }
    }
  };
  this.insert = function(key) {
    var newNode = new Node(key);
    if (root === null) {
      root = newNode;
    } else {
      insertNode(root, newNode);
    }
  }; //向树中插入一个新的键。
  var searchNode = function(node, key) {
    if (node === null) {
      return false;
    }
    if (key < node.key) {
      return searchNode(node.left, key);
    } else if (key > node.key) {
      return searchNode(node.right, key);
    } else {
      return true;
    }
  };
  this.search = function(key) {
    return searchNode(root, key);
  }; //在树中查找一个键,如果节点存在,则返回 true ;如果不存在,则返回false 。
  var inOrderTraverseNode = function(node, callback) {
    if (node !== null) {
      inOrderTraverseNode(node.left, callback);
      callback(node.key);
      inOrderTraverseNode(node.right, callback);
    }
  };
  this.inOrderTraverse = function(callback) {
    inOrderTraverseNode(root, callback);
  }; //通过中序遍历方式遍历所有节点。
  var preOrderTraverseNode = function(node, callback) {
    if (node !== null) {
      callback(node.key);
      preOrderTraverseNode(node.left, callback);
      preOrderTraverseNode(node.right, callback);
    }
  };
  this.preOrderTraverse = function() {
    preOrderTraverseNode(root, callback);
  }; //通过先序遍历方式遍历所有节点。
  var postOrderTraverseNode = function(node, callback) {
    if (node !== null) {
      postOrderTraverseNode(node.left, callback);
      postOrderTraverseNode(node.right, callback);
      callback(node.key);
    }
  };
  this.postOrderTraverse = function() {
    postOrderTraverseNode(root, callback);
  }; //通过后序遍历方式遍历所有节点。
  var minNode = function(node) {
    if (node) {
      while (node && node.left !== null) {
        node = node.left;
      }
      return node.key;
    }
    return null;
  };
  this.min = function() {
    return minNode(root);
  }; //返回树中最小的值/键。
  var maxNode = function(node) {
    if (node) {
      while (node && node.right !== null) {
        node = node.right;
      }
      return node.key;
    }
    return null;
  };
  this.max = function() {
    return maxNode(root);
  }; //返回树中最大的值/键。
  var removeNode = function(node, key) {
    if (node === null) {
      return null;
    }
    if (key < node.key) {
      node.left = removeNode(node.left, key);
      return node;
    } else if (key > node.key) {
      node.right = removeNode(node.right, key);
      return node;
    } else {
      //键等于node.key
      //第一种情况——一个叶节点
      if (node.left === null && node.right === null) {
        node = null;
        return node;
      }
      //第二种情况——一个只有一个子节点的节点
      if (node.left === null) {
        node = node.right;
        return node;
      } else if (node.right === null) {
        node = node.left;
        return node;
      }
      //第三种情况——一个有两个子节点的节点
      var aux = findMinNode(node.right);
      node.key = aux.key;
      node.right = removeNode(node.right, aux.key);
      return node;
    }
  };
  this.remove = function(key) {
    root = removeNode(root, key);
  }; //从树中移除某个键。
}
```

## 图

> 一种非线性数据结构。
> 图是网络结构的抽象模型。

### 创建图类

```js
function Graph() {
  var vertices = [];
  var adjList = new Dictionary();
  this.addVertex = function(v) {
    vertices.push(v);
    adjList.set(v, []);
  };
  this.addEdge = function(v, w) {
    adjList.get(v).push(w);
    adjList.get(w).push(v);
  }; //添加元素
  this.toString = function() {
    var s = '';
    for (var i = 0; i < vertices.length; i++) {
      s += vertices[i] + ' -> ';
      var neighbors = adjList.get(vertices[i]);
      for (var j = 0; j < neighbors.length; j++) {
        s += neighbors[j] + ' ';
      }
      s += '\n';
    }
    return s;
  }; //显示图
  var initializeColor = function() {
    var color = [];
    for (var i = 0; i < vertices.length; i++) {
      color[vertices[i]] = 'white';
    }
    return color;
  };
  this.bfs = function(v, callback) {
    var color = initializeColor(),
      queue = new Queue();
    queue.enqueue(v);
    while (!queue.isEmpty()) {
      var u = queue.dequeue(),
        neighbors = adjList.get(u);
      color[u] = 'grey';
      for (var i = 0; i < neighbors.length; i++) {
        var w = neighbors[i];
        if (color[w] === 'white') {
          color[w] = 'grey';
          queue.enqueue(w);
        }
      }
      color[u] = 'black';
      if (callback) {
        callback(u);
      }
    }
  }; //广度优先搜索
  this.BFS = function(v) {
    var color = initializeColor(),
      queue = new Queue(),
      d = [],
      pred = [];
    queue.enqueue(v);
    for (var i = 0; i < vertices.length; i++) {
      d[vertices[i]] = 0;
      pred[vertices[i]] = null;
    }
    while (!queue.isEmpty()) {
      var u = queue.dequeue(),
        neighbors = adjList.get(u);
      color[u] = 'grey';
      for (i = 0; i < neighbors.length; i++) {
        var w = neighbors[i];
        if (color[w] === 'white') {
          color[w] = 'grey';
          d[w] = d[u] + 1;
          pred[w] = u;
          queue.enqueue(w);
        }
      }
      color[u] = 'black';
    }
    return {
      distances: d,
      predecessors: pred
    };
  }; //优化广度优先搜索

  this.dfs = function(callback) {
    var color = initializeColor();
    for (var i = 0; i < vertices.length; i++) {
      if (color[vertices[i]] === 'white') {
        dfsVisit(vertices[i], color, callback);
      }
    }
  };
  var dfsVisit = function(u, color, callback) {
    color[u] = 'grey';
    if (callback) {
      callback(u);
    }
    var neighbors = adjList.get(u);
    for (var i = 0; i < neighbors.length; i++) {
      var w = neighbors[i];
      if (color[w] === 'white') {
        dfsVisit(w, color, callback);
      }
    }
    color[u] = 'black';
  }; //深度优先搜索
  var time = 0;
  var DFSVisit = function(u, color, d, f, p) {
    console.log('discovered ' + u);
    color[u] = 'grey';
    d[u] = ++time;
    var neighbors = adjList.get(u);
    for (var i = 0; i < neighbors.length; i++) {
      var w = neighbors[i];
      if (color[w] === 'white') {
        p[w] = u;
        DFSVisit(w, color, d, f, p);
      }
    }
    color[u] = 'black';
    f[u] = ++time;
    console.log('explored ' + u);
  };
  this.DFS = function() {
    var color = initializeColor(),
      d = [],
      f = [],
      p = [];
    time = 0;
    for (var i = 0; i < vertices.length; i++) {
      f[vertices[i]] = 0;
      d[vertices[i]] = 0;
      p[vertices[i]] = null;
    }
    for (i = 0; i < vertices.length; i++) {
      if (color[vertices[i]] === 'white') {
        DFSVisit(vertices[i], color, d, f, p);
      }
    }
    return {
      discovery: d,
      finished: f,
      predecessors: p
    };
  }; //优化深度优先搜索
}
```

## 排序和搜索算法

> 排序算法：冒泡排序、选择排序、插入排序、归并排序、快速排序
> 搜索算法：顺序搜索、二分搜索

```js
function ArrayList() {
  var array = [];
  this.insert = function(item) {
    array.push(item);
  }; //插入元素
  this.toString = function() {
    return array.join();
  }; //返回字符串
  var swap = function(index1, index2) {
    var aux = array[index1];
    array[index1] = array[index2];
    array[index2] = aux;
  };
  this.bubbleSort = function() {
    var length = array.length;
    for (var i = 0; i < length; i++) {
      // for (var j = 0; j < length - 1; j++) { //未改进的排序
      for (var j = 0; j < length - 1 - i; j++) {
        if (array[j] > array[j + 1]) {
          swap(j, j + 1);
        }
      }
    }
  }; //冒泡排序（比较相邻元素，前一个大于后一个则交换位置，最终得到升序数组）
  this.selectionSort = function() {
    var length = array.length,
      indexMin;
    for (var i = 0; i < length - 1; i++) {
      indexMin = i;
      for (var j = i; j < length; j++) {
        if (array[indexMin] > array[j]) {
          indexMin = j;
        }
      }
      if (i !== indexMin) {
        swap(i, indexMin);
      }
    }
  }; //选择排序（比较数组类数据，最小的一项与当前循环轮数项交换，最终得到升序数组）
  this.insertionSort = function() {
    var length = array.length,
      j,
      temp;
    for (var i = 1; i < length; i++) {
      j = i;
      temp = array[i];
      while (j > 0 && array[j - 1] > temp) {
        array[j] = array[j - 1];
        j--;
      }
      array[j] = temp;
    }
  }; //插入排序（插入排序每次排一个数组项，以此方式构建最后的排序数组）
  var merge = function(left, right) {
    var result = [],
      il = 0,
      ir = 0;
    while (il < left.length && ir < right.length) {
      if (left[il] < right[ir]) {
        result.push(left[il++]);
      } else {
        result.push(right[ir++]);
      }
    }
    while (il < left.length) {
      result.push(left[il++]);
    }
    while (ir < right.length) {
      result.push(right[ir++]);
    }
    return result;
  };
  var mergeSortRec = function(array) {
    var length = array.length;
    if (length === 1) {
      return array;
    }
    var mid = Math.floor(length / 2),
      left = array.slice(0, mid),
      right = array.slice(mid, length);
    return merge(mergeSortRec(left), mergeSortRec(right));
  };
  this.mergeSort = function() {
    array = mergeSortRec(array);
  }; //归并排序（打散后重新组合）
  var swapQuickStort = function(array, index1, index2) {
    var aux = array[index1];
    array[index1] = array[index2];
    array[index2] = aux;
  };
  var partition = function(array, left, right) {
    var pivot = array[Math.floor((right + left) / 2)],
      i = left,
      j = right;
    while (i <= j) {
      while (array[i] < pivot) {
        i++;
      }
      while (array[j] > pivot) {
        j--;
      }
      if (i <= j) {
        swapQuickStort(array, i, j);
        i++;
        j--;
      }
    }
    return i;
  };
  var quick = function(array, left, right) {
    var index;
    if (array.length > 1) {
      index = partition(array, left, right);
      if (left < index - 1) {
        quick(array, left, index - 1);
      }
      if (index < right) {
        quick(array, index, right);
      }
    }
  };
  this.quickSort = function() {
    quick(array, 0, array.length - 1);
  }; //快速排序
  this.sequentialSearch = function(item) {
    for (var i = 0; i < array.length; i++) {
      if (item === array[i]) return i;
    }
    return -1;
  }; //顺序搜索
  this.binarySearch = function(item) {
    this.quickSort();
    var low = 0,
      high = array.length - 1,
      mid,
      element;
    while (low <= high) {
      mid = Math.floor((low + high) / 2);
      element = array[mid];
      if (element < item) {
        low = mid + 1;
      } else if (element > item) {
        high = mid - 1;
      } else {
        return mid;
      }
    }
    return -1;
  }; //二分搜索
}
```

## 算法补充知识

### 递归

> 递归是一种解决问题的方法，它解决问题的各个小部分，直到解决最初的大问题。
> 通常涉及函数调用自身。

### 动态规划

> 动态规划（Dynamic Programming，DP）是一种将复杂问题分解成更小的子问题来解决的优化技术。

用动态规划解决问题时，要遵循三个重要步骤：

1. 定义子问题；
2. 实现要反复执行而解决子问题的部分（这一步要参考前一节讨论的递归的步骤）；
3. 识别并求解出边界条件。

能用动态规划解决的一些著名的问题如下:

- 背包问题：给出一组项目，各自有值和容量，目标是找出总值最大的项目的集合。这个
  问题的限制是，总容量必须小于等于“背包”的容量。
- 最长公共子序列：找出一组序列的最长公共子序列（可由另一序列删除元素但不改变余
  下元素的顺序而得到）。
- 矩阵链相乘：给出一系列矩阵，目标是找到这些矩阵相乘的最高效办法（计算次数尽可
  能少）。相乘操作不会进行，解决方案是找到这些矩阵各自相乘的顺序。
- 硬币找零：给出面额为 d1…dn 的一定数量的硬币和要找零的钱数，找出有多少种找零的
  方法。
- 图的全源最短路径：对所有顶点对(u, v)，找出从顶点 u 到顶点 v 的最短路径。

### 贪心算法

> 贪心算法遵循一种近似解决问题的技术，期盼通过每个阶段的局部最优选择（当前最好的解），从而达到全局的最优（全局最优解）。

### 大 O 表示法

> 描述算法的性能和复杂程度。
> O(1)：常数的
> O(log(n))：对数的
> O((log(n))c)：对数多项式的
> O(n)：线性的
> O($n^2$)：二次的
> O($n^c$)：多项式的
> O($c^n$)：指数的
