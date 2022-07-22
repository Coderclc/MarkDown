# Frontend

- npm 在操作系统中存在这一指令,而`vue-cli-service` `vite` 直接运行就会报错,当安装包依赖的时候就会在`.bin`下生成对应的可执行文件(软连接)

## JS章节

### 内置类型

- 八种内置类型

  - 基本类型: null undefined string number boolean symbol bigint
  - 引用类型 object

- 数字类型是浮点类型,没有整型,浮点类型基于 IEEE 754标准实现,

- `NaN!=NaN`  `typeof NaN = number`

- 对于基本类型来说，如果使⽤字⾯量的⽅式，那么这个变量只是个字⾯量，只有在必要的时候才会转换为对应的类型

  ```typescript
  let foo = 233 // 这只是字⾯量，不是 number 类型
  foo.toString() // 使⽤时候才会转换为对象类型
  ```

  什么意思呢?要知道233数字可没有toString这个方法,为什么赋值给了foo却拥有了toString这个方法

  首先知道一些等式概念

  ```typescript
  233.hasOwnProperty('toString') // error
  new Number(233).__proto__.hasOwnProperty('toString') // true
  new Number(233) === 233 // false
  Number.prototype.hasOwnProperty('toString') // true
  Number.prototype.__proto__===Object.prototype // true
  Number.prototype.__proto__.hasOwnProperty('toString') // true
  ```


### typeof

- typeof 对于基本类型，除了 null 都可以显示正确的类型

  ```typescript
  typeof 1 // 'number'
  typeof '1' // 'string'
  typeof undefined // 'undefined'
  typeof true // 'boolean'
  typeof Symbol() // 'symbol'
  typeof b // b 没有声明，但是还会显示 undefined
  typeof [] // 'object'
  typeof {} // 'object'
  typeof console.log // 'function'
  typeof null // 'object' 这是⼀个存在很久了的 Bug
  ```

  - 为什么会出现这种情况呢？因为在 JS 的最初版本中，使⽤的是 32 位系统，为了性能考虑使⽤低位存储了变量的类型信息， 000 开头代表是对象，然⽽ null 表示为全零，所以将它错误的判断为 object 。虽然现在的内部类型判断代码已经改变了，但是对于这个 Bug 却是⼀直流传下来。

  - 所以用typeof 来判断类型是不严谨且容易出错的,如果我们想获得⼀个变量的正确类型，可以通过 `Object.prototype.toString.call(xx)` 。这样我们就可以获得类似 `[object Type]` 的字符串。

  - ts 自定义函数需要使用 `is` 关键字用于函数返回值类型中,帮助编译器判断
  
    ```typescript
    function is(val: unknown, type: string) {
      return toString.call(val) === `[object ${type}]`
    }
    
    function isObject(val: any): val is Record<any, any> {
      return val !== null && is(val, 'Object')
    }
    
    function isString(val: unknown): val is string {
      return is(val, 'String')
    }
    ```

  - 判断是否为undefined还有一种方法
  
    ```
    let a
    // 我们也可以这样判断 undefined
    a === undefined
    // 但是 undefined 不是保留字，能够在低版本浏览器被赋值
    let undefined = 1
    // 这样判断就会出错
    // 所以可以⽤下⾯的⽅式来判断，并且代码量更少
    // 因为 void 后⾯随便跟上⼀个组成表达式
    // 返回就是 undefined
    a === void 0
    ```
  

### 类型转换

- 任意类型转Boolean
  - undefined ， null ， false ， NaN ， '' ， 0 ， -0 ，为false其余为true
  - 注意 [] , {} , '0' 为true

- 对象转基本类型

  - 对象在转换基本类型时，⾸先会调⽤对象原型上的 valueOf ,然后调⽤ toString 

    ```
    // 这就是你在控制台经常看到[object Object]这串字符串的原因
    {foo:'foo'} + 'bar' = > [object Object] bar
    ```

  - 当然可以在对象身上重写这两个方法

    ```
    let foo = {
      valueOf(){
        return 0
      },
      toString (){
        return 666
      }
    }
    foo+'233' ->'0233' // 如果valueOf返回基本数据类型则不会调用toString
    
    let foo = {
      valueOf(){
        return this
      },
      toString (){
        return 666
      }
    }
    foo+'233' -> '666233'
    ```

  - 还可以重写 `[Symbol.toPrimitive] `方法,它拥有最高的优先级

    ```
    let foo = {
      valueOf(){
        return this
      },
      toString (){
        return 666
      },
      [Symbol.toPrimitive]() {
        return 233;
      }
    }
    
    foo+'233' -> '233233'
    ```

- 四则运算符

  - \+ 一方为string,则另一方转为string

  - \- \* / 一方为number,另一方转为number

  - +'1' -> 1 number

  - ```
    [1, 2] + [2, 1] // '1,22,1'
    // [1, 2].toString() -> '1,2'
    // [2, 1].toString() -> '2,1'
    // '1,2' + '2,1' = '1,22,1'
    ```

  - 为什么 [] == ![]

    ![type-conversion](C:\Users\Coderclc\Documents\MarkDown\images\type-conversion.png)

    
    
    ```
    1 == true -> true
    2 == true -> false
    !![] -> true
    [] == false
    ```
    
    ```
    // [] 转成 true，然后取反变成 false
    [] == false
    // 根据第 8 条得出
    [] == ToNumber(false)
    [] == 0
    // 根据第 10 条得出
    ToPrimitive([]) == 0
    // [].toString() -> ''
    '' == 0
    // 根据第 6 条得出
    0 == 0 // -> true
    // [1] == [2]  两边都是object 返回false
    ```

- 比较运算符
  - 如果是对象，就通过 toPrimitive 转换对象 
  - 如果是字符串，就通过 unicode 字符索引来⽐较

### 原型

![C:\Users\Coderclc\Documents\MarkDown\images\prototype.png](C:\Users\Coderclc\Documents\MarkDown\images\prototype.png)

### new

- 工厂函数

  ```
  function Person(name, age) {
      var obj = {}
      obj.name = name
      obj.age = age
      obj.run=()=>{
          console.log('i am running');
      }
      return obj
  }
  var foo = Person('foo',18)
  ```

- 构造函数

  ```
  function Person(name, age) {
      this.name = name
      this.age = age
      this.run = () => {
          console.log(this.name + ' running');
      }
  }
  var foo = new Person('foo', 18)
  ```

- new做了什么?

  在调⽤ new 的过程中会发⽣以上四件事情，我们也可以试着来⾃⼰实现⼀个 new	

  1. 新⽣成了⼀个对象
  2. 链接到原型
  3. 绑定 this
  4.  返回新对象

  ```javascript
  function create() {
   // 创建⼀个空的对象
   let obj = new Object()
   // 获得构造函数
   let Con = [].shift.call(arguments) // 空数组执行shift 但把执行对象call为arguments,既把类数组转换为数组并执行shift,且修改了arguments
   // 链接到原型
   obj.__proto__ = Con.prototype
   // 绑定 this，执⾏构造函数
   let result = Con.apply(obj, arguments) // apply的第二个参数为参数数组,可为类数组,既 index:number ,有length 属性
   // 确保 new 出来的是个对象
   return typeof result === 'object' ? result : obj
  }
  // Person 中的this指向Person的调用者.Con
  function Person(name, age) {
    this.name = name
    this.age = age
    this.run = () => {
      console.log(this.name + ' running');
    }
  }
  
  create(Person, 'zone', 18)
  ```

### instanceOf

手写instanceOf

```javascript
function instanceof (left, right) {
  // 获得类型的原型
  let prototype = right.prototype
  // 获得对象的原型
  left = left.__proto__
  // 判断对象的类型是否等于类型的原型
  while (true) {
    if (left === null)
      return false
    if (prototype === left)
      return true
    left = left.__proto__
  }
}
```

### this

- window 
- ()=>{}
- call,bind ,apply

### 执行上下文

当执⾏ JS 代码时，会产⽣三种执⾏上下⽂

- 全局执⾏上下⽂
- 函数执行上下文
- eval执行上下文

```
console.log(foo); // undefined  提升的变量和函数
var foo  = 'foo'
const foo  = 'foo' // error 临时死区
```

### 闭包

函数 A 返回了⼀个函数 B，并且函数 B 中使⽤了函数 A 的变量，函数 B就被称为闭包。

```javascript
function A() {
  let a = 1
  function B() {
    console.log(a)
  }
  return B
}

A()()
// 因为函数 A 中的变量这时候是存储在堆上的。现在的 JS 引擎可以通过逃逸分析辨别出,哪些变量需要存储在堆上，哪些需要存储在栈上。
```

```javascript
for (var i = 1; i <= 5; i++) {
  setTimeout(function timer() {
    console.log(i);
  }, i * 1000);
}

闭包
for (var i = 1; i <= 5; i++) {
  (function (j) {
    setTimeout(function timer() {
      console.log(j);
    }, j * 1000);
  })(i);
}

seTimeout 第三个参数
for (var i = 1; i <= 5; i++) {
  setTimeout(function timer(i) {
    console.log(i);
  }, i * 1000, i);
}

let
for (let i = 1; i <= 5; i++) {
  setTimeout(function timer() {
    console.log(i);
  }, i * 1000);
}
```

### 深浅拷贝

- 浅拷贝

  - Object.assign
  - ...运算符

- 深拷贝

  - JSON.parse(JSON.stringify(object)) 
    - 忽略 undefined
    - 忽略 symbol
    - 不能序列化函数
    - 不能解决循环引⽤的对象

- lodash _.cloneDeep

  ```javascript
  undefined == null // true
  
  const toString = Object.prototype.toString
  
  function getTag(value) {
    if (value == null) {
      return value === undefined ? '[object Undefined]' : '[object Null]'
    }
    return toString.call(value)
  }
  // xxx..toString() 方法，会返回一个形如 "[object XXX]" 的字符串。
  // 但是大多数对象toString()方法都是重写了，这时，需要用 call() 或 Reflect.apply() 等方法来调用。
  ({}).toString();     // => "[object Object]"
  Math.toString();     // => "[object Math]"
  // Object.prototype.toString.call(x);   
  // 准确使用的是Object原型上的toString方法,且通过call改变执行对象
  ```

### 模块化

- es6

  - 异步导⼊，因为⽤于浏览器，需要下载⽂件，如果也采⽤同步导⼊会对渲染有很⼤影响
  - 采⽤实时绑定的⽅式，导⼊导出的值都指向同⼀个内存地址，所以导⼊值会跟随导出值变化

  ```javascript
  // file a.js
  export function a() {}
  export function b() {}
  // file b.js
  export default function() {}
  import {a, b} from './a.js'
  import XXX from './b.js'
  ```

- commonJs

  - 浏览器中使⽤就需要⽤到 Browserify 解析了。

  - 是同步导⼊，因为⽤于服务端，⽂件都在本地，同步导⼊即使卡住主线程影响也不大

  - ⽀持动态导⼊，也就是 require(${path}/xx.js) .

  - 值拷⻉，就算导出的值变了，导⼊的值也不会改变，所以如果想更新

  - 值，必须重新导⼊⼀次。

  ```javascript
  var exports = module.exports
  
  // a.js
  module.exports = {
   a: 1 }
  // or
  exports.a = 1
  // b.js
  var module = require('./a.js')
  module.a // -> log 1
  ```

- amd

### 防抖

- easy

  ```javascript
  const debounce = (func, wait = 50) => {
    let timer = 0
    return function (...args) {
      if (timer) clearTimeout(timer)
      timer = setTimeout(() => {
        func.apply(this, args)
      }, wait)
    }
  }
  ```

  缺点,函数是在wait之后才调用

- hard

  ```
  function debounce(func, wait = 50, immediate = true) {
    let timer, context, args
    const later = () => setTimeout(() => {
      timer = null
      if (!immediate) {
        func.apply(context, args)
        context = args = null
      }
    }, wait)
  
    return function (...params) {
      if (!timer) {
        timer = later()
        if (immediate) {
          func.apply(this, params)
        } else {
          context = this
          args = params
        }
      } else {
        clearTimeout(timer)
        timer = later()
      }
    }
  }
  ```

  缺点,执行的是第一个触发的函数

### 节流







## 数据结构章节

### 链表

- 多个元素组成的列表
- 元素存储不连续，是用过next指针联系在一起的
- 增删数组 ->下标
- 增删链表 -> 改变.next
- 删除链表 替换成下一个删除的值,替换next.next,不能直接将this 修改为 this.next 
- 反转 
  - next.next  = prev  prev = next 指针迭代正序反转   eg  2指向上一次村的1 保存2
  -  return new head next.next.next  = next  next  = null  函数递归到链表的尾部 eg  5指向4 ,打断4的next

- 删除重复 迭代 判断 next.val  === next.next.val? 相同改变指向,否则移动指针
- 环形链表
  - 哈希表 
  - 龟兔赛跑 快慢指针,如果存在环形,那么快指针一定会追上慢指针




## 算法章节

- 时间复杂度  算法的时间复杂度是一个函数,时间复杂度通常用O符号表述.

  - ![[公式]](https://www.zhihu.com/equation?tex=O%281%29): 运行时间和输入大小无关，都在固定时间内算完。
- ![[公式]](https://www.zhihu.com/equation?tex=O%28log%28N%29%29) :我每多提供一倍的麦子，他只多消耗一个格子  比起![[公式]](https://www.zhihu.com/equation?tex=O%28N%29)它更接近![[公式]](https://www.zhihu.com/equation?tex=O%281%29)每操作一次，需要处理的规模就小一半的.既二分搜索
  - ![[公式]](https://www.zhihu.com/equation?tex=O%28N%29) : 随着输入规模的增加，运行时间线性增加。
- ![[公式]](https://www.zhihu.com/equation?tex=O%28Nlog%28N%29%29)：???
  - ![[公式]](https://www.zhihu.com/equation?tex=O%28N%5E2%29) ：随着输入规模的增加，运行时间次方增加。

- 排序方式
  - in-place 占用常数内存，不占用额外内存
  - out-place 占用额外内存


### 冒泡排序

- 俩俩交换，大的放在后面，第一次排序后最大值已在数组末尾。
- 因为俩俩交换，需要`n-1`趟排序，比如10个数，需要9趟排序

```
function bubbleSort(arr) {
  const len = arr.length

  for (let i = 0; i < len - 1; i++) {
    // -1 每一次的最后一个不用比较了 或者j=1比较 j-1
    for (let j = 0; j < len - i - 1; j++) {
      if (arr[j] > arr[j + 1]) {
        ;[arr[j], arr[j + 1]] = [arr[j + 1], arr[j]]
      }
    }
  }

  return arr
}
```

如果第一次没有发生排序,直接返回

```
function bubbleSort(arr) {
  let flag = 1
  const len = arr.length

  for (let i = 0; i < len - 1; i++) {
    for (let j = 0; j < len - i - 1; j++) {
      if (arr[j] > arr[j + 1]) {
        ;[arr[j], arr[j + 1]] = [arr[j + 1], arr[j]]
        flag = 0
      }
    }

    if (flag) return arr
  }

  return arr
}
```



### 插入排序

将一个元素插入到已有序的数组中，在初始时未知是否存在有序的数据，因此将元素**第一个元素看成是有序的**

与有序的数组进行比较，**比它大则直接放入，比它小则移动数组元素的位置，找到个合适的位置插入**

当只有一个数时，则不需要插入了，因此需要`n-1`趟排序，比如10个数，需要9趟排序

```
function insertSort(arr: number[]) {
  // 第一个数不动,其余的插排
  for (let i = 1; i < arr.length; i++) {
    const tmp = arr[i]
    let j = i - 1

    while (arr[j] > tmp) {
      arr[j + 1] = arr[j]
      j--
    }
    arr[j + 1] = tmp
  }
  return arr
}
```

```
function insertSort(arr: number[]) {
  for (let i = 1; i < arr.length; i++) {
    for (let j = i; j; j--) {
      if (arr[j - 1] > arr[j]) {
        ;[arr[j - 1], arr[j]] = [arr[j], arr[j - 1]]
      }
    }
  }
  return arr
}
```



### 选择排序

- 找到数组中最大的元素，与数组最后一位元素交换
- 当只有一个数时，则不需要选择了，因此需要`n-1`趟排序，比如10个数，需要9趟排序

```
function selectionSort(arr) {
  const len = arr.length

  for (let i = 0; i < len - 1; i++) {
    let index = 0

    for (let j = 0; j < len - i; j++) {
      if (arr[j] > arr[index]) {
        index = j
      }
    }
    ;[arr[index], arr[arr.length - 1 - i]] = [arr[arr.length - 1 - i], arr[index]]
  }

  return arr
}
```



### 快速排序

- 迭代归分一分为三

```
function quickSort(array) {
  let pivot = array[array.length - 1]
  let left = array.filter((v, i) => v <= pivot && i != array.length -1)
  let right = array.filter(v => v > pivot)
  return [...quickSort(left), pivot, ...quickSort(right)]
}
```

- 最终情况只有两种  [1,2,3] 基准值为2 ,一次排序成功  基准值为  1 再排 23 ,基准值为 3 再排12

```javascript
function partition(arr, left, right) {
  const pivot = left
  let j = pivot + 1

  //  <= ? len -1
  // 本身为倒序 一直原地交换,j为len -1 基准值与最后交换
  // 本身为正序 不进入判断 , j-1  = pivot
  // 与基准值相等的数会放在基准值的右侧
  for (let i = j; i <= right; i++) {
    if (arr[pivot] > arr[i]) {
      swap(arr, i, j)
      j++
    }
  }

  swap(arr, pivot, j - 1)

  return j - 1
}

function swap(arr, i, j) {
  if (i !== j) {
    ;[arr[i], arr[j]] = [arr[j], arr[i]]
  }
}

function quickSort(arr, left = 0, right = arr.length - 1) {
  if (left < right) {
    const pivotIndex = partition(arr, left, right)
    quickSort(arr, left, pivotIndex - 1)
    quickSort(arr, pivotIndex + 1, right)
  }

  return arr
}
```



### 希尔排序

- 希尔排序实质上就是插入排序的增强版

```
function shellSort(arr) {
  var gap = Math.floor(arr.length / 2)

  while (gap) {
    for (var i = gap; i < arr.length; i++) {
      var j = i

      while (j > 0 && arr[j - gap] > arr[j]) {
        // eg 十一个数 既gap = 5  0,6,11 插排
        // eg 4个数两两交换无法获得正确排序,当通过从小到大的插排即可实现  2->4->6->8
        ;[arr[j], arr[j - gap]] = [arr[j - gap], arr[j]]
        j -= gap
      }
    }

    gap = Math.floor(gap / 2)
  }

  return arr
}
```





1. 两数之和 哈希表
2. 学生分数的最小差值 排序＋滑动窗口
3. 回文数 
   - x和y同时修改 ,x<y
   - 要么x和y为同位数,要么y一定比x多一位
4. 无重复字符的最长子串 将On*m 改为 On次 ,left,right 双指针
5. 有序数组中的单一元素 二分法 因为 mid>=left 所以left+1 mid  =Math.floor((right - left) / 2) + left 防止超出范围  偶数^1 奇数^1 &1妙用
6. 罗马数字转整数 全部枚举
7. 整数转罗马数字 枚举+递减 
8. 最长公共前缀 ASIIC排序以后,求第一个和最后一个的并集
9. 有效的括号 有序采用堆栈 
10. 删除有序数组中的重复项 快慢指针
11. 移除元素 二分法 二分法比直接遍历快
12. 实现StrStr KMP 算法 找前缀函数,BM 算法
13. 找出星型图的中心节点 认真读题即可
14. 搜索插入位置 二分法判断
15. 最大子数组和 求max Math.max MAX_SAFE_INTEGER ,min ....
16. 最后一个单词的长度 while(i--) 
17. 加一 保存进位
18. 二进制求和 保存进
19. x的平方根 也是采用二分法判断
20. 验证回文串 ^\da-zA-Z 写好正则表达
21. 买卖股票的最佳时机 求max
22. 只出现一次的数字 
    - 任何数和 0 做异或运算，结果仍然是原来的数
    - 任何数和其自身做异或运算，结果是 0
23. 多数元素 摩尔投票法 求众数 一一消耗不为自身消耗剩下的肯定是众数
24. Excel 表列序号 String.fromCharCode 'A'.charCodeAt(0)
25. Excel 表列名称 余数范围0~25 A的范围为 1~26 %10 /10 所以%26 /26
26. 快乐数 哈希循环
27. 同构字符串 双哈希表 (foo.has(x) && foo.get(x) !== y) || (bar.has(y) && bar.get(y) !== x)
28. 存在重复元素 计算数组长度比较
29. 存在重复元素II 哈希表判断
30. 第一个错误版本 二分法判断
31. 移动零 双指针 [left,right]  =[right,left]
32. 单词规律 双哈希表 
33. Nim 游戏 先手后手都将剩余数控制为 1~3 即为4的倍数
34. 反转字符串  [left,right]  =[right,left]
35. 赎金信 new Array(26).fill(0) 统计法
36. 仅仅反转字母 [...string]
37. 字符串中的第一个唯一字符
38. 找不同
    - 求和 new Array.fill(0) 遍历 一旦 --后<0 即为多数
    - 求和 ASCII 一个＋一个-
    - 位运算 0^x = x  x^x = 0
39. 判断子序列 双指针
40. 二进制手表
    - 排列 *A**n**m*=*n*×(*n*−1)×(*n*−2)×…×(*n*−*m*+1)=*n*!/(*n*−*m*)!
    - 组合 *C**n**m*=*m*!*A**n**m*=*n*!/*m*!×(*n*−*m*)!
41. 找到所有数组中消失的数字 鸽笼法 index 替换为负
42. 最小操作次数使数组元素相等  使n-1 个数字加1 ===使n个数字-1
43. 寻找两个正序数组的中位数  合并有序数组后求中位
44. 合并两个有序数组  双指针判断大小,
45. 考试的最大困扰度 滑动窗口 累加 超出k既左移
46. 消失的数字 找异或
47. DP(Dynamic programming) 动态规划 把原问题分解为相对简单的子问题的方式来就求解

    cell\[i]\[j] = Math.max(上一个单元格的价值(cell\[i-1][j]),当前商品的价值+剩余空间的价值(上一个单元格的剩余空间价值))

    ```javascript
    function findMaxTest() {
      const commoditys = ['', 'guitar', 'sound', 'laptop', 'phone']
      const lbs = [0, 1, 4, 3, 1]
      const prices = [0, 1500, 3000, 2000, 2000]
      const backpacks = Array.from(new Array(5), () => new Array(5).fill(0))
    
      for (let x = 1; x <= 4; x++) {
        for (let y = 1; y <= 4; y++) {
          const previousPrice = backpacks[x - 1][y]
    
          if (lbs[x] > y) {
            backpacks[x][y] = previousPrice
          } else {
            const currentPrice = prices[x] + backpacks[x - 1][y - lbs[x]]
            backpacks[x][y] = Math.max(previousPrice, currentPrice)
          }
        }
      }
    
      function findMax(x, y) {
        if (x) {
          if (backpacks[x][y] === backpacks[x - 1][y]) { // 当前的价值由上一个来
            findMax(x - 1, y)
          } else { // 当前价值由自身加磅数差最大值而来 backpacks[x][y] === (prices[x] + backpacks[x - 1][y - lbs[x]])
            console.log(commoditys[x], prices[x]);
            findMax(x - 1, y - lbs[x]) // 磅数差
          }
        }
      }
    
      findMax(4, 4)
    }
    
    
    findMaxTest()
    ```

    



## Git 章节



