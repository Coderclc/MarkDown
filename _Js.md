# Js

[toc]

## String

- substr(start,length) 

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

