# _TypeScript

[toc]

## 基础类型

- 任意类型

  ```typescript
  const foo: any = ???
  ```

- 数字类型

  ```typescript
  const foo: number = 233
  ```

- 字符类型

  ```typescript
  const foo: string = 'hello world!'
  ```

- 布尔类型

  ```typescript
  const flag: boolean = true
  ```

- 枚举类型

  ```typescript
  enum Color { Red, Green, Blue, }  // 0,1,2
  ```

- 数组类型

  ```typescript
  const arr: number[] = [1,2]
  or
  const arr: Array<number> = [1,2]
  ```

- 元组类型

  ```typescript
  const tuple:[string,number] = ['hello world!', 233] // 对应位置,数量须相同
  ```

- void 类型

  ```typescript
  function hello(): void {
      alert("Hello Runoob");
      return null || undefined 
  }
  
  const hello = (): void => {
    alert("Hello Runoob");
      return null || undefined 
  };
  
  // 无返回值 或者返回 return null || undefined 
  ```

- null类型

  ```typescript
  const foo: null = null
  // null 为空对象的引用
  // typeof -> object
  // 是任何类型的子类型（包括 void）
  ```

- undefined类型

  ```typescript
  const foo: undefined = undefined
  // undefined 没有设置值的变量
  // typeof undefined -> undefined
  // 是任何类型的子类型（包括 void）
  ```

- never类型

  ```typescript
  let x: never
  // never 为其它类型（包括 null 和 undefined）的子类型,只能赋值为never
  
  // 返回类型为error
  function error(message: string): never {
      throw new Error(message);
  }
  
  // 无法达到的z
  function infiniteLoop(): never {
      while (true) {
      }
  }
  
  ```
  
- 对象类型

  ```typescript
  const user: object = { name:"chenlicheng",age:18 }
  但是通过.访问属性
  user.name // Property 'name' does not exist on type 'object'.
  
  resolve
  1. const user: any = { name:"chenlicheng",age:18 }
  2 user['name']
  3 interface  真正的用法
  4 断言 (user as any).name  (<any>user).age
  ```

- 联合类型

  ```typescript
  const foo: number|string
  
  const arr: (number|string)[]
  const arr: Array<number|string> 
        
  const arr: Array<number>|Array<String> = []
  ```



## 变量声明

```typescript
var [变量名] : [类型] = 值;
```

### 类型断言

```typescript
gramma format
<类型>值
or
值 as 类型

let foo = 'foo';

foo = 233 as any
foo = <any> 233

function getLength(target: number | string): number {
  if ((target as string).length || (<string>target).length) { // 必须断言,number 为.l
  } else {
    return target.toString().length;
  }
}

// 当x>y 既y为x的子集,那么 x能断言为y,如果你希望y断言为x,那么你可以使用any,但这样是不安全的
```

### 类型推断

```typescript
let foo = 'foo';

foo = 233; // Type 'number' is not assignable to type 'string'.ts(2322)

// 没有给出类型的时候,编译器会利用类型推断推出类型
// 若不能推断默认为any
```

### 变量作用域

- 全局作用域
- 局部作用域
- 类作用域



## 运算符

- 算术

  ```
  + - * / % ++ --
  ```

- 逻辑

  ```
  && || !
  ```

- 关系

  ```
  == != > < >= <=
  ```

- 按位

  ```
  & | ~ ^ << >> >>>
  ```

- 赋值

  ```
  = += -= *= /=
  ```

- 三元/条件

  ```
  ()?():()
  ```

- 字符串

  ```
  - +
  ```

- 类型

  ```
  typeof instanceof
  ```



## 条件语句

- if
- if else
- if else-if else
- switch case



## 循环

```
for(init;condition;increment){}
```

```
for(var i in j)
```

```
for(var i of j)
```

```
forEach every some...
```

```
while(condition){}
```

```
do{}while(condition)
```

```
break // 能有效提升循环性能
```

```
continue
```

``` 
for(;;){} while(true){} 无线循环
```



## 函数

- 参数个数,类型限制,返回值限制

  ```
  function add(x: number, y: number): number {
  	return x + y;
  }
  ```

- 可选参数必须跟在必需参数后面,参数不能同时设置为可选和默认。

  ```
  function add(x: number = 100, y?: number): number {
      return x + y;
  } 
  ```

- 剩余参数

  ```
  function foo(...arg: Array<any>){}
  ```

- 函数定义

  ```
  function foo (){}
  ```

- 匿名函数,将匿名函数赋值给一个变量

  ```
  const foo = ()=>{}
  ```

- 构造函数

  ```
  var myFunction = new Function("a", "b", "return a * b"); 
  var x = myFunction(4, 3); 
  console.log(x);
  ```

- 递归函数

  ```
  function factorial(number) {
      if (number <= 0) {         // 停止执行
          return 1; 
      } else {     
          return (number * factorial(number - 1));     // 调用自身
      } 
  }; 
  console.log(factorial(6));      // 输出 720
  ```

- 函数重载

  ```
  function disp(s1:string):void; 
  function disp(n1:number,s1:string):void; 
   
  function disp(x:any,y?:any):void { 
      console.log(x); 
      console.log(y); 
  } 
  disp("abc") 
  disp(1,"xyz");
  
  // 如果参数类型不同，则参数类型应设置为 any。
  // 参数数量不同你可以将不同的参数设置为可选。
  ```



## Map

```
let myMap = new Map([
  ["key1", "value1"],
  ["key2", "value2"]
]); 
```

- map.clear() – 移除 Map 对象的所有键/值对 。
- map.set() – 设置键值对，返回该 Map 对象。
- map.get() – 返回键对应的值，如果不存在，则返回 undefined。
- map.has() – 返回一个布尔值，用于判断 Map 中是否包含键对应的值。
- map.delete() – 删除 Map 中的元素，删除成功返回 true，失败返回 false。
- map.size – 返回 Map 对象键/值对的数量。
- map.keys() - 返回一个 Iterator 对象， 包含了 Map 对象中每个元素的键 。
- map.values() – 返回一个新的Iterator对象，包含了Map对象中每个元素的值 。

```
for (let i of Iterator) or Iterator.next()
```



## 元组



