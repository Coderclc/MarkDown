

- js 可选参数: undefined 占位

- ts可选参数 ? 可选参数后面不能再出现必须参数
- 可选参数和默认值不能同时
- 声明类型定义的时set可选,面向类型时set默认值

```
type Sum = (num1: number, num2?: number) => number
let fn: Sum = (x, y = 1) => x + y
type interface 类型定义只能设置可选,在面向的时候添加默认值.或者使用的时候判断undefined
```

```
function fn(num1: number, num2: number = 3): number {
  return num1 + num2
} 
fn(1)
```








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




类装饰器

```
function foo(constructor: Function) {}

@foo
class Foo {
	constructor() { }
}

```

类装饰器工厂

```
function foo(params: string) {
	return (constructor: Function) => {
		params
		constructor
	}
}

@foo('bar')
class Foo {
	constructor() { }
}
```



类型别名

```

type Name = string;
type NameResolver = () => string;
type NameOrResolver = Name | NameResolver;
type EventNames = 'click' | 'scroll' | 'mousemove'; //还能面向具体值
function getName(n: NameOrResolver): Name {
    if (typeof n === 'string') {
        return n;
    } else {
        return n();
    }
}
```





