<script>
# ES5
每一个对象实例都有两种属性，一个是自己的实例属性一个是原型属性
Person.prototype = clc.__proto__
1. Object.keys()
clc= {name:'chenlicheng',age:18}
Object.keys(clc) = [name,age] instance of Array
2.obj.hasOwnProperty('key')  return boolean

新增Object接口
对象 构造器 说明
Object getPrototypeOf 返回对象的原型
Object getOwnPropertyDescriptor 返回对象自有属性的属性描述符
Object getOwnPropertyNames 返回一个数组，包括对象所有自有属性名称集合（包括不可枚举的属性）
Object create 创建一个拥有置顶原型和若干个指定属性的对象
Object defineProperty 给对象定义一个新属性，或者修改已有的属性，并返回
Object defineProperties 在一个对象上添加或修改一个或者多个自有属性，并返回该对象
Object seal 锁定对象。阻止修改现有属性的特性，并阻止添加新属性。但是可以修改已有属性的值。
Object freeze 冻结对象，阻止对对象的一切操作。冻结对象将永远不可变。
Object preventExtensions 让一个对象变的不可扩展，也就是永远不能再添加新的属性。
Object isSealed 判断对象是否被锁定
Object isFrozen 判断对象是否被冻结
Object isExtensible 判断对象是否可以被扩展
Object keys 返回一个由给定对象的所有可枚举自身属性的属性名组成的数组
Object.setPrototypeOf(clc, prototype) clc.__proto__ = 参数二prototype
clc.__protp__ = why.__proto=Object.prototype 所有的对象都是类Object的实例

新增Array接口
indexOf 返回根据给定元素找到的第一个索引值，否则返回-1
lastIndexOf 方法返回指定元素在数组中的最后一个的索引，如果不存在则返回 -1
every 测试数组的所有元素是否都通过了指定函数的测试-检测数组中的所有元素是否都大于 10,返回boolean
some 测试数组中的某些元素是否通过了指定函数的测试-检测在数组中是否有元素大于 10,返回true or false
forEach
filter
map
reduce
reduceRight 从右到左
Array.isArray(arr)
arr instanceof Array

JSON对象
var test = {
   "name": "gejiawen",
   "age": 22
};
JSON.strinfy(test) ->JSON字符串
JSON.parse('{"name": "larry"}') ->json对象


protype 原型对象
function Person(){
  this.name = name
  console.log(this)
}
Person() this->windows
new Person("chenlicheng") this -> Person{name:"chenlicheng"}
加了关键字 new  返回一个对象,这个对象的this 为Person 中的this

es5 之前 构造函数
function Person(name) {
  const obj ={}
  obj.name = name
  return obj
}
引入new 关键字new
function Person(name) {
  this.name = name;
  this.run=function(){
    console.log(this.name +"running");
  }
}
this.run()高度开辟空间,把它添加到函数的原型中
Person.prototype.run=function(){
  console.log(this.name +"running");
}


super 关键字
1.this和super的区别：
this关键词指向函数所在的当前对象
super指向的是当前对象的原型对象
Object.prototype.flag = "我在proto中"
const clc = {
  flag:"我在对象clc中",
  fn(){
    console.log(super.flag);
    console.log(this.flag);
  }
}clc.fn()
2.super != Object.getPrototypeOf(this) 获取这个对象的原型对象
虽然都是指向原型对象,但此时,super的this为包含super的this
Object.getPrototypeOf(this) 原型对象的this,为原型对象

class Person{
  constructor(name){
    this.name = name }
  run(){}
}
Person.prototype.walk = function(){}
const clc = new Person('chenlicheng')
属性在clc实例对象上,方法在__proto__上 

class students extends Person{
  constructor(age){
    super('chenlicheng')
    this.age=age
  }
}
const clc = new students('18')  //students {name: "chenlicheng", age: "18"}
super()相当于调用父类的constructor(),并且要在所有之前
所以类 students.prototype.__proto__ == 类Person.prototype
类students .prototype 为 类Person的实例
# ES6
一.let const var 
let const 赋予了{}作用域
var a = 2;
{
  let a = 3;
  console.log(a); // 3
}
console.log(a); // 2

let,const 关键词声明的变量不具备变量提升（hoisting）特性
常量 const 声明时，推荐使用：CAPITAL_CASING
const 声明要有初始值,let不必

二、arrow function

三、函数参数默认值
function clc (name = 'chenlicheng'){}

四、...拓展运算符 spread/rest
spread  作为实参
function foo(x,y,z) {
  console.log(x,y,z);
}
let arr = [1,2,3];  foo(...arr); // 1 2 3  把arr数组中的所有元素提取到对应位置
rest作为形参
function foo(...args) {
  console.log(args);
}
foo( 1, 2, 3, 4, 5); // [1, 2, 3, 4, 5] 所有传进来的参数会放到args这个数组中

五对象词法拓展
1.对象中 key:value 相同可简写
2. 函数简写
3. 属性可以使用表达式计算值 ['make' + make]: true, key加中括号可写表达式,变量

六、 二进制和八进制字面量
let oValue = 0o10;
console.log(oValue); // 8

let bValue = 0b10; // 二进制使用 `0b` 或者 `0B`
console.log(bValue); // 2

七、对象和数组的解构
const [a,b,c] = [1,2,3]

const { clc: { name:cnmae='123', age } } = foo()

cname = ???||123

解构对象中的对象中的属性 使用属性可以给默认值的同时换名字

const { clc: { name:cnmae='123', age } } = foo()

解构对象中的对象,

const { clc = { name: '123', agee: '456' } } = foo() 

当clc=undefined时 clc = { name: '123', agee: '456' } 赋予默认值值在clc为不存在时赋予,即使赋予了name...gender:'male' 当clc存在时,gender也为undefined

八、对象中使用super. 
const obj = {
  name : "chenlicheng",
  fn(){
    console.log(this.name);
    console.log(super.name);//wuhaiyan
  }
}
Object.prototype.name = "whuhaiyan"
obj.fn()

九、 模板语法和分隔符
`***${}***`

十 . for...of VS for...in

十一 Map 和 WeakMap  新的数据结构集
MAP
var map = new Map()
var str = 'str'
var obj = {}
var fun = function(){}
map.set(str,1)
console.log(map);  一种映射
map.size = 1内置 size 属性   {"str" => 1}
console.log(map.get(str)); map.set map.get 读书设值
WEAK MAP
WeakMap 就是一个 Map，只不过它的所有 key 都是弱引用，意思就是 WeakMap 中的东西垃圾回收时不考虑，使用它不用担心内存泄漏问题。
WeakMap 的所有 key 必须是对象。它只有四个方法 delete(key),has(key),get(key) 和set(key, val)：
var wmap = new WeakMap()
var o = {
  value: 1,
}
wmap.set(o,1)
console.log(wmap);


十二 Set 和 WeakSet
Set 对象是一组不重复的值，重复的值将被忽略，值类型可以是原始类型和引用类型：
const cSet = new Set([1,2,3,4,5,1,2,3,4,5])
console.log(cSet) ; {1,2,3,4,5}
console.log(cSet.size); 5
cSet.has(6): boolean
cSet.add('123')
cSet.add({name:'clc'})
console.log(cSet); {1,2,3,4,5,'123',obj}

weakSet  key 只能为 obj

十三、类   
static 添加方法到函数的属性,也可以添加基本数据
extends  继承 父类的 constructor 和 方法 配合super() 使用
类的方法添加到类的原型对象,
子类的实例.__proto__.proto__ = 父类的原型
子类的构造函数中 super指向原型对象为父类的实例,对应实例中的constructor函数
class Person {
  a = 2  //公共属性
  constructor() {
    console.log("executing");
  }
  run() {
    console.log("running");
  }
  static jump() {
    console.log("jumping");
  }
}
class students extends Person{
  constructor(){
    super()
    super.run()
    super 指向父类的实例, 实例可访问父类中的方法
  }
}
const why = new students()
console.log(typeof Person);  //function
const clc = new Person()
clc.run()  //添加到Person 的原型对象中
Person.jump() //添加到Person 函数的属性
类的声明不会提升（hoisting)，

class Person{
  a = 2
  constructor(b){
    console.log(this.a)
    this.b = b
  }
}
const clc = new Person()
// 实例公共属性a  每创建一个实例,都会执行一次类的constructor,执行完默认返回一个实例
constructor 内添加的属性为私有属性 this指向实例
class Example {
    constructor() {
        this.sum = (a, b) => {
            console.log(a + b);
        }
    }
}
实例方法,将方法添加到实例上
decorator
decorator 是一个函数，用来修改类的行为，在代码编译时产生作用。

getter 与setter
class Example{
    constructor(a, b) {
        this.a = a; // 实例化时调用 set 方法
        this.b = b;
    }
    get a(){  存取值函数
        console.log('getter');
        return this.a;
    }
    set a(a){
        console.log('setter');
        this.a = a; // 自身递归调用
    }
}
设置a 时访问执行set,属性访问a执行get,类似proxy
子类不写constructor时,默认自动调用super()

十四 Symbol
var s1 = Symbol("clc")
var s2 = Symbol("clc")
var obj = {
  [s1] : 'why',
  [s2] : 'why'
}
{
  Symbol(clc): "why"
Symbol(clc): "why"
}
var s1 =  Symbol('why')
var s2 = Symbol('why')
console.log(s1==s2);//false


十五  迭代器（Iterators）
var arr = [1,2,3,4,5]
var itr = arr[Symbol.iterator]()
console.log(itr.next());  {value:1 ,done:false}  done表示迭代状态
console.log(itr.next());  {value:2 ,done:false}
...
console.log(itr.next());  {value:5 ,done:false}
console.log(itr.next());  {value:undefined ,done:true}

十六 . Generators
允许一个函数返回的可遍历对象生成多个值。
在使用中你会看到 * 语法和一个新的关键词 yield:
function *num(){
  let c = 1
  while(true){
    yield c++
  }
}
var clc = num()   clc = num {<suspended>}
console.log(clc.next()); {value: 1, done: false}
console.log(clc.next());  {value: 2, done: false}
每次执行 yield 时，返回的值变为迭代器的下一个值。

十七. Promises 
new Promise((resolve,reject)=>{
  resolve()
  reject()
}).then(res=>{

}).catch(err=>{

})
十八 、Reflect 与 Proxy
Proxy 与 Reflect 是 ES6 为了操作对象引入的 API 
Proxy 可以对目标对象的读取、函数调用等操作进行拦截，然后进行操作处理
Reflect 可以用于获取目标对象的行为，它与 Object 类似，但是更易读，
var target = {
  name: "why",
  age: 18,
}
var handler = {
  get: function (target, key, proxy) {
    console.log("getting")
    return target[key] 
    //proxy == Proxy() 实例
  },
  set: function (target, key, value) {
    console.log("setting ")
    target[key] = value
  },
}
let proxy = new Proxy(target, handler)
proxy.name 
//why proxy 代理是没有name这个属性的,带访问name时,执行handler中的get函数,自动传入target,key,proxy三个参数
// proxy.age = 25 // 实际执行 handler.set

target 可以为空,后面通过代理set
proxy.name='clc' set proxy.name get

handler 也可以为空,此时相当于没有拦截

Reflect
let exam = {
  name: "Tom",
  age: 24,
  get info(){
      return this.name + this.age;
  }
}
console.log(Reflect.get(exam, 'name')); //tom
let receiver = {
    name: "Jerry",
    age: 20
}
Reflect.get(exam, 'info', receiver);  jerry 20 改变this绑定

十九 、查找字符串
ES6 之前判断字符串是否包含子串，用 indexOf 方法，ES6 新增了子串的识别方法。
includes()：返回布尔值，判断是否找到参数字符串。
startsWith()：返回布尔值，判断参数字符串是否在原字符串的头部。
endsWith()：返回布尔值，判断参数字符串是否在原字符串的尾部。
let string = "apple,banana,orange";
string.includes("banana");     // true
string.startsWith("apple");    // true
string.endsWith("apple");      // false
string.startsWith("banana",6)  // true
如果需要知道子串的位置，还是得用 indexOf 和 lastIndexOf 并且index可传正则,新加的这些不行

字符串重复 repeat() 
const str = 'clc'
console.log(str.repeat(2)); //clcclc

padStart：返回新的字符串，表示用参数字符串从头部（左侧）补全原字符串。
padEnd：返回新的字符串，表示用参数字符串从尾部（右侧）补全原字符串。
console.log("h".padStart(5,"o"));  // "ooooh"
console.log("h".padEnd(5,"o"));    // "hoooo"
console.log("h".padStart(5));      // "    h"

二十 Object.assign(target, source_1, ···)
let target = {a: 1};
let object2 = {b: 2};
let object3 = {c: 3};
Object.assign(target,object2,object3);  
// 第一个参数是目标对象，后面的参数是源对象
target;  // {a: 1, b: 2, c: 3
同名属性，则后面的属性会覆盖前面的属性。

thisArg 上一个函数执行的this对象
find((item = >item>2)   返回第一个符合条件的
findIndex() 返回第一个符合条件的index

函数,类都有一个name属性,即类名,函数名



# es2020

1. **try catch 新格式，允许不写error*

2. 可选链 x.prop1?.prop2  不用担心是否存在,不存在会返回undefined

3. String # matchAll 可以返回一个迭代器,替代 reg.exec

   const regexp = /[a-c]/g  const str = 'abc'

   const iterator = str.matchAll(regexp)

   Array.from(iterator,res=>log(res))