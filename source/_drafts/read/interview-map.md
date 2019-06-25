---
title: '前端面试指南'
category: 兴趣
tags: [阅读笔记]
date: 2019-06-10
---

ESBI，我们一生的财富...

<!-- more -->

## 2019-06-10 读书笔记

### JS 内置类型

基础类型：number、string、Boolean、null、undefined、symbol
引用类型：object

### 类型转换

转 Boolean，在条件判断时，除了 undefined， null， false， NaN， ''， 0， -0，其他所 有值都转为 true，包括所有对象。
对象在转换基本类型时，首先会调用 valueOf 然后调用 toString。

==操作符
比较运算 x==y，其中 x 和 y 是值，产生 true 或者 false，这样比较按如下方式进行：

1. 若 Type(x)与 Type(y)相同（xy 的类型相同），则
   a. 若 Type(x)为 undefined，返回 true。
   b. 若 Type(x)为 Null，返回 true。
   c. 若 Type(x)为 Number，则
   i. 若 x 为 NaN,返回 false
   ii. 若 y 为 NaN,返回 false
   iii. 若 x 与 y 为相同数值,返回 true
   iv. 若 x 为+0 且 y 为-0,返回 true
   v. 若 x 为-0 且 y 为+0,返回 true
   vi. 返回 false
   d. 若 Type(x)为 String，则当 x 和 y 为完全相同的字符序列（长度相等且相同字符在相同位置）时返回 true。否则，返回 false。
   e. 若 Type(x)为 Boolean，当 x 和 y 同为 true 或者同为 false 时返回 true，否则返回 false。
   f. 当 x 和 y 为引用同一对象时返回 true。否则，返回 false
2. 若 x 为 null 且 y 为 undefined，返回 true
3. 若 x 为 undefined 且 y 为 null，返回 true
4. 若 Type(x)为 Number 且 Type(y)为 String，返回 comparison x==ToNumber(y)的结果。
5. 若 Type(x)为 String 且 Type(y)为 Number，
6. 返回比较 ToNumber(x)==y 的结果。
7. 若 Type(x)为 Boolean，返回比较 ToNumber（x）==y 的结果
8. 若 Type(y)为 Boolean，返回比较 x==ToNumber（y） 的结果
9. 若 Type(x)为 String 或 Number，且 Type(y)为 Object，返回比较 x==ToPrimitive(y)的结果。
10. 若 Type(x)为 Object 且 Type(y)为 String 或 Number，返回比较 ToPrimitive(x)==y 的结果。
11. 返回 false

注释：ToPrimitive 是对象转基本类型
总结：弱类型比较类型不一样就转成数字来比较。
