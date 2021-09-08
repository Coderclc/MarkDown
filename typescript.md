export{} 导出一个对象,这个文件会被视为一个模块,有自己的作用域



TsLint 推荐上面 

object 类型
const info: object = {
  name:"clc",
  age:20
}
但是此时访问info.name会报错,所以不加object,让其自动类型推断

symbol 类型
const person = {
  identity:"programmer",
  identity:"teacher"
}  err
const s1: symbol = Symbol("identity")
const s2: symbol = Symbol("identity")
const person = {
[s1]:"programmer",
[s2]:"teacher"
}
{Symbol(identity): "programmer", Symbol(identity): "teacher"}
Object.keys(),Object.getOwnPropertyNames(),for in for of ,stringfy 都获取不到对象中的symol键
可用Object.getOwnPropertySymbols()  Reflect.ownKeys() 获得

Symbol.for()  能够创建相同的 s1 == s2
Symbol.keyFor() 找全局注册的字符串

numm and undefined
const n: null = null
const u: undefined = undefined


Typescript 数据类型
 enum 枚举类型  处理非数值的数据
      enum DIRECTION {EAST,SOUTH, WEST,NORTH}
      const d1: DIRECTION = DIRECTION.EAST
      const d2: DIRECTION = DIRECTION.WEST
      默认的值是从 0开始 0,1,2,3,如果EAST = 10 ,SOUTH = 11
      也可以通过值访问名称  DIRECTION[VALUE]
tuple 元组类型  原来放不同类型的数组,并且定死了长度,与python中的不同
      const tInfo: [string,number,number] =["clc",18,18]
      const item1 = tInfo[0] "clc" 并且知道clc为string
      const arr2: Array<string|number> = ['1',2]
      const item2 = arr2[2] 2 但是类型丢失
      当添加越界的元素时，它的类型会被限制为元组中每个类型的联合类型：string|number
any 类型
    let a: any = "why"
      a = 12  可发生类型变换
    const aarr: any[] = ['1',2]
    const aarr: Array<any> = [1, '2']

void 类型
let v: voidv = undefined  v = null
function return undefined null
undefined null 为其他基础类型的子类型, config nullchecks 之后 num可设置为空

never 类型
    函数时一个死循环,没出来 ,或者抛出异常,那么函数的类型为nerver
    const clc: (num: any)=>never = (num:string|number)=>{
    while(true){
      console.log(123);
    }
    }
    const clc: () => never = ()=>{
   throw new Error('err')
    }
 let foo = (()=>{
  throw new Error('error')
})()
let num: number = 123
num = foo
never 类型为所有类型的子类型   



TS函数
函数声明 function declaration

function clc(num1: number, num2: number): number {
  return num1 + num2
}
函数表达式 function expression
const clc = (num1: number, num2: number): number => {
  return num1 + num2
}
并不正确的
只对等号右侧的匿名函数进行了类型定义，而等号左边的 mySum，是通过赋值操作进行类型推论而推断出来的。
相当于
const clc: (num1: number, num2: number) => number = (x, y) => {
  return x + y
}相当于
const clc: (num1: number, num2: number) => number = function(x, y){
  return x + y
}相当于

当函数没有返回值时,函数的类型为void

let fn: (name: string, age: number) => number
fn=(x,y)=>{
  return y
}
type CLC = (name: string, age: number) => number
let fn: CLC
fn=(x,y)=>{
  return y
}
js 可选参数位置可以任意,但是要传undefined占位
TS,可选参数后面不允许再出现必需参数了：
type Sum = (num1: number, num2?: number) => number
let fn: Sum = (x, y = 1) => x + y

function fn(num1: number, num2: number = 3): number {
  return num1 + num2
} 函数声明直接写默认值即可 fn(1)
console.log(fn(1,2));  不仅要给默认值,type还要改为可选参数

let obj = {
  '0':'clc',
  '1':18,
  length:2
}
Array.prototype.slice.apply(obj);  ['clc',18]
把一个伪数组变成数组


[] 元组 (number|string)[] 数组 Array<number|string>
type T  type Arr = <T>(x: T) => T
对应函数表达式可写any,也可以不写

let num
num = 4
num = '5'

 let num = 4 num = '5' error 类型推断 

(<anywindow).foo = 1;
console.log((window as any).foo);


函数类型
const clc = new Function()  面向一个类,就是面向一个类的实例的接口
run:() => void 
run:Function
this.run=()=>{}

Class  类
pubilc 实例公共属性(值传入)     直接写属性  实例公共属性 值默认
static 静态属性  放在类的对象
extends 继承  子类的原型 = new 父类 的实例  
        在子类中访问父类的方法,this指向子类实例
super() 调用父类的constructor
super原型对象 在子类中的函数,构造函数中,super调用父类原型的方法,
      在子类静态方法中 ,super调用父类对象上的方法
存取器  getter  setter    public  name  get name()  set  name()
private  私有属性  只能在类中访问,无法再内外部访问
private 可修饰构造函数,该类不允许被继承或者实例化
protected 子类可以访问  constructor this.attr
protected 构造函数 父类无法被实例化,只能实例化子类

构造函数参数中
public name: string = 类中 public name:string + 构造函数体 this.name = name
readonly 同理 但readonly 只能读不能写  最好写成public readonly

抽象类  abstract  Class  和protected constructor 一样,无法直接实例,只能通过子类继承实例化
在
抽象方法 public abstract sayHi():void; 只能在抽象类中
此时抽象方法子类必须实现,即同名 定义方式类似接口 

声明文件
声明文件必需以 .d.ts 为后缀。
// src/jQuery.d.ts
declare var jQuery: (selector: string) => any; 声明
// src/index.ts
jQuery('#foo');   使用

@types 统一管理第三方库的声明文件
npm install @types/jquery --save-dev   在tools工具页面搜索所需的文件

类型别名
type Name = string;
type NameResolver = () => string;
type NameOrResolver = Name | NameResolver;
type EventNames = 'click' | 'scroll' | 'mousemove'; 还能面向具体值
function getName(n: NameOrResolver): Name {
    if (typeof n === 'string') {
        return n;
    } else {
        return n();
    }
}
声明合并 ->函数重载
使用eslint  http://ts.xcatliu.com/engineering/lint.html

  内部模块  命名空间

        namespace clc { export function why(){}}
        clc.why()
外部模块   模块


装饰器:特殊的类型声明,能够附加到类声明,方法属性,参数上,修改类的行为
类装饰器,属性装饰器,方法装饰器,参数装饰器
写法,普通装饰器无参数,装饰器工厂 可传参


普通装饰器  添加
function foo(iclass: any) {
  console.log(iclass);
  iclass.prototype.age = 18
  iclass.prototype.run=()=>{
    console.log("running");
  }
}
@foo
class Parent {
  constructor() { }
}
const clc:any = new Parent()
console.log(clc.age);
clc.run()
类装饰器,会把类传入函数foo,并执行foo函数

装饰器工厂
function foo(params: string) {
  return (iclass: any) => {
    console.log(params);
    console.log(iclass);
  }
}
@foo('clc')
class Parent {
  constructor() { }
}


类装饰器修改原先的类
function foo(iclass: any) {
  return class extends iclass {
    name: string = "why"
    run(){
      console.log("runningwhy");
    }
  }
}

@foo
class Parent {
  public name: string
  constructor() {
    this.name = "clc"
  }
  run() {
    console.log(this.name + "running");
  }
}

const clc = new Parent()
console.log(clc);
clc.run()
修改了原先类的方法和属性


属性装饰器
