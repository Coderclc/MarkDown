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



## 接口

- 接口一般首字母大写。tslint建议加上I前缀, 

  ```
  interface IPerson {
    firstName: string
    lastName: string
    sayHi: () => string
    run(): number
  }
  // 属性不能少,不能溢出
  ```

- 可选属性和只读属性

  ```
  interface Person {
    name?: string,
    readonly age: number,
    run?(): void,
  }
  const why: Person = {
    // name 键值对缺失不会报错
    age: 18
  }
  why.run&&why.run() //判断函数执行
  why.age++  //修改age报错 Cannot assign to 'age' because it is a read-only property.
  ```

- 任意类型

  ```
  interface Person {
    name: string,
    age?: number,
    [index: string]: any
  }
  
  const why: Person = {
    name: 'why',
    age: 18,
    gender:'female'
  }
  
  ```

  - index 只是一个占位符
  - 任意类型可以少,可以溢出
  - 任意类型的类型必须包含其余属性的类型

- 联合类型和接口

  ```
  interface IRunOptions { 
    program:string; 
    commandline:string[]|string|(()=>string); 
  } 
  ```

- 接口和数组

  ```
  interface INamelist { 
    [index:number]:string 
  } 
  
  interface ages { 
     [key:string]:number   // 伪数组
  } 
  // 索引值可以是数字或字符串
  ```

- 单接口继承

  ```
  interface Person {
    age: number
  }
  
  interface Musician extends Person {
    instrument: string
  }
  ```

- 多接口继承

  ```
  interface IParent1 { 
    v1:number 
  } 
  
  interface IParent2 { 
    v2:number 
  } 
  
  interface Child extends IParent1, IParent2 { } 
  // 逗号分隔符分割
  ```

- 面向接口和类型断言

  ```
  interface IUser {
    name: string
    age: number
  }
  
  const user: IUser = {} // error  issing the following properties
  
  const user = {} as IUser // true
  ```

- 接口与函数

  ```
  const foo: (name: string, age: number) => string = (name: string, age: number): string => {
    return `name : ${name}, age: ${age}`
  }
  // 给变量foo定义了函数类型,并且把一个定义了类型的匿名函数赋值给他
  
  // 定义两个接口
  interface IUser {
    name: string,
    age: number,
  }
  
  interface IUserFunc {
    (user:IUser):string
  }
  // or
  type IUserFunc = (user: IUser) => string
  
  // next
  const foo: IUserFunc = user => {
    return `name : ${user.name}, age: ${user.age}`
  }
  ```

- 注意区别

  ```
  interface IUserFunc {
    (): string
  }
  // 一个函数,函数返回值为string
  
  interface IUserFunc {
    foo(): string
  }
  // 一个对象,对象里有foo这个函数,返回值为string
  ```

- 类实现接口

  ```
  interface Skr {
    name: string,
    age: number,
    rap():void
  }
  class Person {
    name
    constructor(name: string) {
      this.name = name
    }
  }
  class Rapper extends Person implements Skr{
    age
    constructor(name: string, age: number) {
      super(name)
      this.age = age
    }
    rap(){
      console.log('I can sing and dance tap');
    }
  }
  // constructor 还是需要定义类型限制,否则仍然无法限制
  ```



## 类

### 类的声明

```
class User {
  name
  age
  gender: string = 'male'
  constructor(name: string, age: number, gender?: string) {
    this.name = name
    this.age = age
    gender && (this.gender = gender)
  }
  run(): void {}
}
```

### 类的继承

子类除了不能继承父类的私有成员(方法和属性)和构造函数，其他都可以继承。一次只能继承一个,但可以多重继承

```
class User {
  name
  age
  constructor(name: string, age: number) {
    this.name = name
    this.age = age
  }
  run(): void {}
}

class Student extends User {
  gender
  phone
  constructor(name: string, age: number, gender: string, phone: number) {
    super(name, age)
    this.gender = gender
    this.phone = phone
  }
}
```

### 继承类的重写

```
class PrinterClass { 
   doPrint():void {
      console.log("父类的 doPrint() 方法。") 
   } 
} 
 
class StringPrinter extends PrinterClass { 
   doPrint():void { 
      super.doPrint() // 调用父类的函数
      console.log("子类的 doPrint()方法。")
   } 
}
```

### 关键字

- static  定义方法或属性在类名本质是一个函数上

- readonly 只读属性
- public 默认为公有的
- private 只能在定义类中使用
- protected 只能在子父类中访问



## 对象

- 在typescript中往对象身上添加属性会编译错误,因为ts对象必须是特定类型的实例,

  ```
  var sites = {
      site1: "Runoob",
      site2: "Google",
      sayHello: function () { } // 类型模板
  };
  sites.sayHello = function () {
      console.log("hello " + sites.site1);
  };
  sites.sayHello();
  // 提前声明类型模板
  // 面向一个字符字符索引接口
  ```



## 命名空间

```
namespace SomeNameSpaceName {
  export interface ISomeInterfaceName {}
  export class SomeClassName {}
}

SomeNameSpaceName.SomeClassName

export default SomeNameSpaceName
or
export namespace SomeNameSpaceName {
  export interface ISomeInterfaceName {}
  export class SomeClassName {}
}
```



## 声明文件

- 在ts 中使用第三方的js,无法使用ts 的类型检查功能

  ```
  declare var jQuery: (selector: string) => any;
  
  jQuery('#foo');
  使用 declare 关键字来定义它的类型，帮助 TypeScript 判断我们传入的参数类型对不对
  ```

- 声明文件以.d.ts 结尾



## 泛型

- 不预先指定具体类型,而在使用的时候再指定

  ```
  export {}
  type IGetFunc = (...args: Array<number|string>)=>(number|string)[]
  
  let getArr:IGetFunc
  
  getArr = (...args)=>{
    const arr = []
    arr.push(...args)
    return arr
  }
  
  getArr('foo','bar').forEach(item=>{
    item.length // error Property 'length' does not exist on type 'number'.
  })
  // 使用类型断言,函数重载,any有些许本末倒置
  ```

- 声明时声明\<T>,调用的时候指定类型

  ```
  type IGetFunc = <T>(...args: Array<T>)=>T[]
  
  let getArr:IGetFunc
  
  getArr = (...args)=>{
    const arr = []
    arr.push(...args)
    return arr
  }
  
  getArr<string>('foo','bar').forEach(item=>{
    item.length 
  })
  ```

- 不手动指定则类型自动推论

  ```
  getArr('foo','bar').forEach(item=>{
    item.toFixed(1) // error
    // Property 'toFixed' does not exist on type 'string'. Did you mean 'fixed'
  })
  ```

- 泛型参数可指定多个

  ```
  type Func = <T, U>(x: T, y: U) => [U, T]
  let swap: Func = (x, y) => {
    return [y,x]
  }
  swap(1,'1'); // ['1',1]
  ```

- 泛型约束

  ```
  type IFunc =<T extends string>(x:T)=>T
  
  const foo:IFunc = x=>{
    x.length // right T 默认为any,无法访问 sting.length
    return x 
  }
  
  foo('foo').length
  ```

- 泛型继承接口

  ```
  interface Bar {
    length: number
  }
  function foo<T extends Bar>(x: T): T {
    x.length
    return x
  }
  foo('foo') // ✔
  foo({ length: 233 }) // ✔
  // 限制了T需拥有length这个属性,而非T为一个对象
  ```

- 多个泛型参数之间的约束

  ```
  function foo<T, U extends keyof T>(obj: T, attr: U): T {
    console.log(obj[attr]);
    return obj
  }
  const bar = {
    name: 'bar'
  }
  foo(bar, 'name')
  foo(bar, 'age') // error 类型“"age"”的参数不能赋给类型“"name"”的参数。
  keyof为ts在泛型定义时独有的关键字
  ```

- 泛型T默认值

  ```
  function foo<T = number>(x: T): T {
    return x
  }
  不指定或者无法推测时,将会使用默认值
  ```

- 泛型与接口

  - 形参前,或接口名后

  ```
  interface Arr {
    <T>(...args: T[]): Array<T>
  }
  or
  interface Arr<T>{
    (...args: T[]) :Array<T>
    attr:T
  }
  // 第二种在面向时需手动定义泛型类型
  ```

  ```
  type Arr = <T>(...args: T[]) => Array<T>
  or
  type Arr<T> = (...args: T[]) => Array<T>
  ```

- 泛型与类

  ```tsx
  class Person<T = string> {
    name: T
    constructor(name: T) {
      this.name = name
    }
    run(): T {
      const foo: T = this.name
      return foo
    }
  }
  const why = new Person<string>('why')
  ```



## 装饰器
