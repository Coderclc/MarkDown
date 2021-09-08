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
  }
  
  const hello = (): void => {
    alert("Hello Runoob");
  };
  
  // 无返回值
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
  4
  ```

- 多类型

  ```typescript
  const foo: number|string
  
  const arr: (number|string)[]
  const arr: Array<number|string> 
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

