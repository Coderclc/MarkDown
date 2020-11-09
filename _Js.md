# Js

[toc]

ECMASCRIPT + DOM + BOM

## Basic

- NaN!=NaN

- isNaN() return Boolean

- 关系运算符 两边皆为str 时比较unicode,按位比较

- label 嵌套循环跳到指定位置
- 有符号整数,32位为符号位,0为正数,1为负数

- 负数是用二进制的补码存储的  补码即为绝对值,取反➕1
- 左移 有符号,无符号<< 左移动  左移不会影响符号位,-2 左移为-64,空缺补0 
- 右移 有符号右移  左边空出,补的是符号位的值 对于正数来说,结果相同
- - 无符号右移    空缺位补0
- 基本数据类型在栈,引用数据类型在堆 创建变量开辟栈,创建对象开辟堆,   引用数据类型在栈里存的值是堆的地址 
- 比较object == 比较的是在栈中的地址
- js函数有类函数签名,形参实参
- fun默认返回undefined
- 全局变量为window的属性 ,全局方法为window的方法
- 声明提前 const foo = function(){} function foo(){} 不同
- [],'0' 布尔值为1
- script 标签属性 defer 先下载后执行  async 下载的同时渲染
-  document.write 会覆盖整个页面
- 函数属性prototype指向原型对象,原型对象constructor 指向函数

## String

- substr(start,length) 
- split() 可传递reg, 返回数组
- search() 可传递reg,返回匹配内容 g无效
- replace() 替换 可传递reg

## Array

- find() 回调return true,返回元素.此后的元素不会再触发函数
- filter()
- map()
- reduce()
- some()   任一返回true,停止迭代
- every() 回调皆为true,则返回true
- flat() 扁平化



## Object 

- assign()  (target,sources,sources)  后者覆盖前者



## Dom

- cloneNode() 拷贝一个节点 传true 递归复制子孙节点,否则只复制当前节点
- @touchstart @touchmove @touchend  针对移动端的事件
- querySelector 无论什么 selector 都只返回第一个匹配项
- querySelectorAll aggregate

- return false 取消浏览器默认行为
- 从外往内捕获 ,从内向外冒泡 微软认为从内向外传播,网景认为从外向内创播事件的传播  
- btn.addEventListener("click",clc,false)  传参数 fa'l'se可改变传播方向
- event=event||window.event取消冒泡 event.cancelBubble=true;
- event 事件的委派
- innerHTML 所有节点  innerText 文本节点

-  body=document.body  html=document.documentelement  document.all =getelementbytagname("*")
- 



## Ajax

asynchronous javascript  and xml

```
var xhr = new XMLHttpRequest()
xhr.open("get","url")
xhr.setRequestHeader("Content-Type","application/x-www-form-urlencoded")
xhr.send(json{} or urlencoded)
xhr.onload=function(){xhr.responseText}
```

- xhr.responseText 类型为JSON字符串
- 传输数据格式 x-www-form-urlencoded 和Json

- xhr.readyState()  0请求了但未初始化,即未调用open(),1已初始化未发送 2 已经发送未响应 3正在接受响应4响应完成v

- xhr.onreadystatechange()状态码改变时触发兼容ie,效率低. xhr.onload() capture respond 触发
- xhr.status http状态码 200ok  400 server 500 network
- 



## RegExp

-  exec将()赋予 Regexp.$1.....$9

- /igsm  ignore 忽略大小写  global 全局模式 s . 匹配空白符 multiline 多行模式
- [.-] 匹配.或者- 
- [A-Z0-9] 所有字母和数字
- .?懒惰匹配 .* 贪婪匹配
- \b 单词边界
- (n) 捕获 
- (?:n) 不捕获,返回的整体包含这一部分
- (?=n) 不捕获,返回的整体也不包含
- /n(?!233)/ 捕获 不紧跟着233 的n
- /n(<=233)/ 捕获前面紧跟着233 的n
- /n(<!233)/ 之后
- ?<n> 给组命名







## practical skills

- 低版本ie auto cache ,在router拼接随机str
- better-scroll
- 防抖debounce 将上一个定时器关闭  clearTimeout(timer);timer = setTimeout(() => {console.log("我只执行了一次");}, 300);  

```
debounce(fun, delay) {
    let timer 
    return (...args) => {
        timer && clearTimeout(timer)
        timer = setTimeout(() => {
            fun.apply(this, args)
        }, delay)
    }
}
```



- 节流 throttle

