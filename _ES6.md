# _ES6

<<<<<<< HEAD
## 一、let和const

- 有作用域
- 不能重复声明
- 不存在变量提升

## 二、解构赋值

```
let [a, ...b] = [1, 2, 3];
//a = 1
//b = [2, 3]
```

对象同理可如此解构, 或者delete  obj.key

## 三、Symbol

- 独一无二的值

  ```
  let sy = Symbol("KK");
  console.log(sy);   // Symbol(KK)
  typeof(sy);        // "symbol"
   
  // 相同参数 Symbol() 返回的值不相等
  let sy1 = Symbol("kk"); 
  sy === sy1;       // false
  ```

- 做obj key保证不重复

- ```
  const COLOR_BLUE = "blue";
  const MY_BLUE = "blue";
  当常量相同时,并不独特,可用symbol改写
  ```

## 四、Map与Set

- Map 对象保存键值对。任何值(对象或者原始值) 都可以作为一个键或一个值。
- map key是有序的
- key
  - 字符串
  - 对象
  - 函数
  - Nan

- Set 对象允许你存储任何类型的唯一值，无论是原始值或者是对象引用。

- Set 应用

- ```
  数组去重复
  var mySet = new Set([1, 2, 3, 4, 4]);
  [...mySet]; // [1, 2, 3, 4]
  并集
  var a = new Set([1, 2, 3]);
  var b = new Set([4, 3, 2]);
  var union = new Set([...a, ...b]); // {1, 2, 3, 4}
  交集
  var a = new Set([1, 2, 3]);
  var b = new Set([4, 3, 2]);
  var intersect = new Set([...a].filter(x => b.has(x))); // {2, 3}
  差集
  var a = new Set([1, 2, 3]);
  var b = new Set([4, 3, 2]);
  var difference = new Set([...a].filter(x => !b.has(x))); // {1}
  ```

## 五、Reflect 与 Proxy

Proxy 可以对目标对象的读取、函数调用等操作进行拦截，然后进行操作处理。它不直接操作对象，而是像代理模式，通过对象的代理对象进行操作，在进行这些操作时，可以添加一些需要的额外操作。

Reflect 可以用于获取目标对象的行为，它与 Object 类似，但是更易读，为操作对象提供了一种更优雅的方式。它的方法与 Proxy 是对应的。

## 六、String

- **includes()**：返回布尔值，判断是否找到参数字符串。
- **startsWith()**：返回布尔值，判断参数字符串是否在原字符串的头部。
- **endsWith()**：返回布尔值，判断参数字符串是否在原字符串的尾部。
- repeat()：返回新的字符串，表示将字符串重复指定次数返回。
- **padStart**：返回新的字符串，表示用参数字符串从头部（左侧）补全原字符串。
- **padEnd**：返回新的字符串，表示用参数字符串从尾部（右侧）补全原字符串。

=======
正式名称es2015,以后,包括统称es6

## babel转码,导入,配置

## let 和const

- 有作用域
- 不存在变量提升
- 暂时性死区 区块中存在`let`和`const`命令，这个区块对这些命令声明的变量，从一开始就形成了封闭作用域。凡是在声明之前就使用这些变量，就会报错。例如如果typeof undefined,但是如果多了let 报Reference error
- 不允许重复声明
>>>>>>> e5f5405ec1f6645ee6cd9fbb708a2a47d21e7522
