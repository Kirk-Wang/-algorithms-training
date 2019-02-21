# ALGORITHMS-TRAINING

这是一个用来算法训练的玩具

[![Build Status](https://travis-ci.org/Kirk-Wang/algorithms-training.svg?branch=master)](https://travis-ci.org/Kirk-Wang/algorithms-training) &nbsp; [![Coverage Status](https://coveralls.io/repos/github/Kirk-Wang/algorithms-training/badge.svg?branch=master)](https://coveralls.io/github/Kirk-Wang/algorithms-training?branch=master)


### 时间复杂度

**算法依赖模型**

我们假定 CPU 会顺序的执行所有的指令，而内存随机访问的代价是相同的，例如：

而与内存最相近的数据结构就是数组，那么我们认为，对于任何一个我们定义的数组：

```js
const a = [1, 2, 3, 4, 5]
```

它的索引操作，占用 `1` 单位时间（也就是消耗 1 的 CPU 指令）

```js
a[2]
```

对象的赋值

```js
const obj = {} // 创建对象的成本
obj['x'] = 1 // 1 次索引，1 次赋值
```

我们同样不能简单认为是 1 的时间，而是要具体问题具体分析

```js
const d = new Date()
```

`但我们认为上述操作都是耗时很少的操作，可以在常数时间内执行完成`

因为 CPU 通常提供一些指令，比如加减乘除，所以我们可以认为下列操作可以在 1 的时间内完成：

```js
1 + 2
100 + 200
499 * 21
500/3
10%5
```

但对一些更加复杂的操作，就不能这样认为了：

```js
"123" + "456"
Math.pow(10, 10)
Math.sqrt(100)
```

`但我们通常可以认为这些操作也是相对较快的常数级别操作`

我们认为一部分逻辑运算符也可以在 1 的单位时间计算完成：

```js
1 > 2
a > b
x <= 3
```

**线性时间的算法**

从一个有序数组中搜索一个值，最暴力的方法就是遍历了。当然也是最慢的做法。我们来分析下这个算法的复杂度，我们下面来分析一下的运行时间。

```js
function find(arr, value) {
  for (let i=0;i<arr.length;i++) {
    if (arr[i] === value) {
      return value
    }
  }
  return null
}
```

在`最坏`的情况下，没有找到值：

* 第 2 行：`i=0` 执行了 `1` 次；`i<arr.length` 执行了 `N+1` 次; `i++` 执行了 `N` 次。所以说总共执行了 `2N+2` 次。
* 第 3 行：比较操作执行了 N 次
* 第 4 行：执行 0 次
* 第 7 行：执行 1 次

所以算法的最坏的情况下，用时：T = 2N + 2 + N + 1 = 3N + 3

这种最坏的情况下，复杂度和数据规模 N 相关的算法很常见，我们称为线性时间复杂度。

**100W 整数数据的排序**

* 先生成 1-100W 的整数
* 写一个算法将他们随机打乱
* 再写一个算法对他们进行排序
* 最后输出一下自己程序的总执行时间

**大数定理**

* 在随机事件的大量重复出现中，往往呈现几乎`必然`的规律，这个规律就是大数定律
* 比如抛硬币，次数多了之后（比如 `1` 万次），正面朝上和反面朝上的数量会趋同

**需要用到的两个希腊字母**

* 算法复杂度的衡量用到 3 个字母，分别是 `O`，`Θ(theta)`，`Ω(omega)` 是两个希腊字母

**复杂度的表示**

算法通常执行时间是一个区域，算法的执行时间，空间消耗，会随着输入规模的变化而变化，我们用下面的术语来描述这种变化关系：

* O：渐进上界
  * f(n) = O(g(n))
  * 先前寻找值的函数时间复杂度是 `3N+2`, 我们这里就记为 `O(n)`
    * 不用关心这个常量，因为它是一条直线
    * `4N+2` 或者 `5N+2` 总是在 `3N+2` 的上面，它们就是这个函数的渐进上界
  * `3N^2 + N + 5` -> `O(N^2)`
  * 衡量最坏的情况（通常关心这个）
* Ω：渐进下界
  * 先前寻找值的函数时间复杂度是 `3N+2`, `N` 等于 0 时，就是常量规模的
* Θ：渐进紧密界
  * `fisherYatesShuffle`，没有更坏的情况了，`O：渐进上界` 与 `Ω：渐进下界` 都控制在了 `N` 这个级别，紧密的边界

一般研究的是`O：渐进上界`
* O(1), 是常数阶
* O(N)
* O(N^2)
* O(nlgn)
* O(n!)
* ...

**线性关系O(n)**

* y=ax+b
* 比如说一个数列查找最大值，复杂度是O(n)，算法执行时间随着规模增长是线性关系

**二次函数关系O(n^2)**

||O(n)|O(n^2)|
|:---------|:---------|:---------:|
|10|10|100|
|100|100|10^4|
|1000|1000|10^6|
|10000|10000|10^8|
|100000|100000|10^10|

**插入排序(慢)**

* 循环不变式：(每次循环结束后，达到了一个什么样的要求？)
  * 每次循环结束，存在一个已经排序的列表和一个未排序的列表，`j` 指向下一个未排序的数字
  * | 已排序 |   未排序   |

* 插入排序的复杂度分析
  * 最好情况，所有正序Ω(n)
  * 最坏情况，所有倒序O(n^2)
  * 平均情况：(n^2)

**Divide&Conquer（分治）**

* 分：将问题分解成子问题，子问题规模变小但问题不变
* 治：递归解决子问题，子问题的子问题，当子问题足够小，就直接解决
* 合：合并子问题的解
* 代表
  * 归并排序，快速排序


**快速排序的循环不变式**

[小于支点][大于支点][未确认]

### 前端算法数据结构的场景

**图相关算法**

rollup 使用 tree-shaking 算法，检测用不到的代码，减小包的大小

**树（DOM-DIFF）算法**

**队列和调度算法（React Fiber）**

* [Fiber vs Stack Demo](https://claudiopro.github.io/react-fiber-vs-stack-demo/)
* requestAnimationFrame

**图论（Webpack split chunk plugin 的计算）**

**图形算法**

* SVG 和 Canvas 绘图底层的算法，衍生出 d3.js, highcharts, echarts, canvas.js 等等一些列的图标库；以及构成 html 中渲染的基础
* [http://cubic-bezier.com/](http://cubic-bezier.com/)

**数据可视化算法**

**3D相关算法**

* tree.js[https://github.com/marmelab/tree.js]

**随机访问存储器**

* 你可以把计算机的内存想象成一个非常大的数组，你可以像读取数组中元素一样读取内存中的值。读取内存中任意位置的值，消耗的时间是相同的。

----

### 编码技巧

* 递归控制
* 循环控制
* 边界控制
* 数据结构

#### 在白板上写程序

* 程序写在：白板，纸笔，Word文档，记事本……
* 修改不便；缩进不便；对齐困难；
* 心里不抵触；先思考后写；不要惧怕修改/重写

#### 数学归纳法

`用于证明断言对所有自然数成立`

* 证明对于 N=1 成立
* 证明 N>1 时：如果对于 N-1 成立，那么对于 N 成立

`求证：1+2+3+...+n=n(n+1)/2`

* 1 = 1*2/2
* 如果 1+2+3+...+(n-1) = (n-1)n/2
* 那么 1+2+3+...+n = 1+2+3+...+(n-1)+n
* = (n-1)n/2+n = (n(n-1)+2n)/2 = n(n+1)/2
* 映射成程序
  * int sum(int n) {
  * if(n==1) return 1;
  * return sum(n-1) + n;}

#### 数学归纳法的正确性

* 公理

#### 递归控制

* 如何证明递归函数正确执行？
  * 数学归纳法中的数学/自然语言 <--> 程序语言

#### 递归书写方法

* 严格定义递归函数作用，包括参数，返回值，Side-effect
* 先 `一般` ，后 `特殊`
* 每次调用 `必须` 缩小问题规模
* 每次问题规模缩小程度必须为 `1`



---

### DOM-Diff 简单实现

[深度剖析：如何实现一个 Virtual DOM 算法](https://github.com/livoras/blog/issues/13)

**实现步骤**

1. 用JS对象模拟DOM树
2. 比较两棵虚拟DOM树的差异
3. 把差异应用到真正的DOM树上

**DFS（有兄弟👬，有儿子，先找儿子🐻）**

### A* 算法

**A* 估价函数**

* f(n) = g(n) + h(n)
  * f(n) 是 n 节点的估价函数
  * g(n) 是初始节点到 n 节点的实际代价
  * h(n) 是 n 节点到目标点的实际代价

**A* 算法程序实现**

* open 队列
  - 排序估价函数
* close 队列
  - 排除干扰节点
* 查询相邻位置
* 封装估价函数f() g() h()
* 设置父节点指针

---

### 上✋玩具

[文档](https://o-o.ren/algorithms-training/index.html)

安装
```sh
npm i algorithms-training
```

使用
```js
import { 
  reverseWords,
  countBinarySubstrings,
  letterCombinations,
  hasGroupsSizeX,
} from 'algorithms-training'
console.log(reverseWords(`Let's take LeetCode contest`))
// s'teL ekat edoCteeL tsetnoc
console.log(countBinarySubstrings("00110011"))
// 6
console.log(letterCombinations("23"))
// ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"]
console.log(hasGroupsSizeX([1,2,3,4,4,3,2,1]))
// true
```

### 开发实验环境准备
- 快速开始一个规范的 NPM 包
  * [typescript-library-starter](https://github.com/alexjoverm/typescript-library-starter)
- Link
  * [npm](https://www.npmjs.com/)
  * [Travis CI](https://travis-ci.org/)
  * [Coveralls](https://coveralls.io/)

### 字符串

* [557. 反转字符串中的单词 III](https://leetcode-cn.com/problems/reverse-words-in-a-string-iii/)

  * 知识点
    * String.prototype.split
    * String.prototype.match
    * Array.prototype.map
    * Array.prototype.reverse
    * Array.prototype.join
    
* [696. 计数二进制子串](https://leetcode-cn.com/problems/count-binary-substrings/)

  * 思路
    * 仔细找输入与输出的关系，把输出往输入里面套，形成图谱后进行规律分析。
    * 找题目所要求的子串，从原字符串 0 位开始
      * 正则匹配连续 0 或者 1
      * 反转 0 或者 1，跟在后面形成[题目所要求的子串]，进行正则匹配
      * 后移一位，从[新的字符串]中继续[找题目所要求的子串]，直到[原字符串]位移完毕

  * 知识点
    * String.prototype.slice
    * String.prototype.match
    * String.prototype.repeat
    * Array.prototype.push
    * RegExp

### 数组

* [17. 电话号码的字母组合](https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/)

  * 思路
    * 把输出往输入里面套，明显就是一个组合问题
    * 根据数字字符串，找到映射字符串，reduce 两两组合，最终形成所有的组合

  * 知识点
    * Array.prototype.reduce

* [914. 卡牌分组](https://leetcode-cn.com/problems/x-of-a-kind-in-a-deck-of-cards/)

  * 认真读题
  * 思路
    * 排序
    * 按数字分组，记录`长度最小`的组
    * return 各分组`长度`是否能被整除


### A & Q
#### 难度大的算法题目如何解？
算法的本质是寻找规律并实现
#### 如何找打规律？
发现输入与输出的关系，寻找突破点
#### 复杂的实现怎么办？
实现是程序+数据结构的结合体
