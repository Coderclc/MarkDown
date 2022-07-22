# Review

- 全局上下文,web 下var 变量,function函数会添加到window,const,let不会添加,nodejs var不会添加到global ,函数上下文,var,let ,const 都不会添加到全局,但二者不写关键字都会添加到全局,全局变量和是否添加到全局对象上不冲突

- count++ 如果count为undefined返回NAN

- ex 就是css中的一个相对单位, 相对的是字体大小和字体样式而改变的一个单位 

- GET和POST的区别? get：使用URL传递参数；发送信息的数量有限制；post：所发送的数据的大小理论上是没有限制，post 可以发送纯文本、URL编码格式、二进制格式的字符串

- Math.random

  - 0~1 包括0,不包含1
  - 0~10 Math.floor(Math.random()*10) 不包含10
  - 2~10 Math.floor(Math.random()*(10 - 2)) + 2

- let [a,b, c,d, e] = ``"hello"``;  数组可以解构字符串

- Html5 的存储对象 localStorage sessionStorage

- window.onload

- \<script>放在<head>和放到<body>底部的区别,head 优先加载,但是无法操作body里的元素,且加载慢的时候会阻塞

- defer 和 async dom的加载和style和script的下载是同步的,影响用户体验.JavaScript 线程和 GUI 线程是互斥的

  - defer 用于开启新的线程下载脚本文件，并使脚本在文档解析完成后执行。多个defer按照文档顺序
  - async 用于异步下载脚本文件，下载完毕立即解释执行代码多个async根据先加载先解析原则

- new 操作符做了什么

  - 创建空对象
  - 链接原型
  - 绑定this
  - 返回新对象

- session 和cookie记住登录机制的原理

  - cookie 客户端的状态保存机制 通过cookie里携带的用户信息识别用户
  - session  服务端的状态保存机制 通过cookie里携带sessionId 通过sessionId 识别用户

- 网页中接收事件的顺序（事件流）有哪些？它们之间的区别是什么？

  - 冒泡 向上传递
  - 捕获 相下传递

- 跨域,网页发起的请求与网页的协议,域名,端口有一样不同就是跨域请求,原因?浏览器为了保证网页的安全，出的同源协议策略。解决方法?

  - cors：目前最常用的一种解决办法，通过设置后端允许跨域实现。
    res.setHeader('Access-Control-Allow-Origin', '*');
    res.setHeader("Access-Control-Allow-Methods", "GET, PUT, OPTIONS, POST");

    node中间件、nginx反向代理：跨域限制的时候浏览器不能跨域访问服务器，node中间件和nginx反向代理，都是让请求发给代理服务器，静态页面面和代理服务器是同源的，然后代理服务器再向后端服务器发请求，服务器和服务器之间不存在同源限制。

    JSONP：利用的原理是script标签可以跨域请求资源，将回调函数作为参数拼接在url中。后端收到请求，调用该回调函数，并将数据作为参数返回去，注意设置响应头返回文档类型，应该设置成javascript。

    postmessage：H5新增API，通过发送和接收API实现跨域通信。

- cookie ,localStorage,sessionStorage的区别

  - 都是浏览器的本地存储
  - cookie通常是由服务端写入,并且决定生命周期,LocalStorage是写入就一直存在，除非手动清除，SessionStorage是页面关闭的时候就会自动清除
  - cookie的存储空间比较小大概4KB,storage 5MB
  - 都遵循同源原则, sessionStorage必须是同一个页面
  - 发送请求会自动携带cookie,storage不会
  - 应用场景  Cookie一般用于存储登录验证信息SessionID或者token，LocalStorage常用于存储不易变动的数据，减轻服务器的压力,SessionStorage可以用来检测用户是否是刷新进入页面，如音乐播放器恢复播放进度条的功能。

- 基本数据类型和引用数据类型的根本区别.

  - 基本数据类型是直接存储在栈中的简单数据段，占据空间小，属于被频繁使用的数据。
  - 引用数据类型是存储在堆内存中，占据空间大。引用数据类型在栈中存储了指针，该指针指向堆中该实体的起始地址，当解释器寻找引用值时，会检索其在栈中的地址，取得地址后从堆中获得实体
  - BigInt 的使用方式 1. 整数后面直接➕n 2. BigInt('')构造函数

- setTimeout(foo, 0) 这行代码不可以等价替换为 foo()  同步变异步 不能相互转换

- window.requestAnimationFrame  你希望执行一个动画，该回调函数会在浏览器下一次重绘之前执行,回调函数执行次数通常是每秒 60 次 既  setInterval(function(){ },1000/60)  requestAnimationFrame  相比 setInterval 1. 会把每一帧中的所有DOM操作集中起来，在一次重绘或回流中就完成 2.会在在后台标签页或者隐藏的iframe里时暂停调用以提升性能和电池寿命。

  无限重绘动画

  ```
  ;(function animloop() {
  	render()
  	window.requestAnimationFrame(animloop)
  })()
  ```

- Object.defineProperty configurable、enumerable、writable 不指定默认为false node环境下不指定enumerable看不到对象的key,value,浏览器环境下还是看得到,如果对象已经有了这个key,再指定时,不指定的不会变成false

- js 严格模式 出厂的时候太松散了,后加的对弱语言的限制 [了解JS严格模式，对你没坏处！-阿里云开发者社区 (aliyun.com)](https://developer.aliyun.com/article/975537)

  - 整个文件开启	

    ```
    <script>
      "use strict";
      console.log("严格模式");
    </script>
    ```

  - 单个函数开启

    ```
    function strict() {
      "use strict";
      return "严格模式";
    }
    ```

  - 一个项目多个脚本文件,有的开启有的没开启,打包完成以后合并的代码属于什么模式?

    - 建议按照一个个的函数去开启严格模式。

    - 所有代码都放到立即执行的匿名函数中

      ```
      (function (){
        "use strict";
      })();
      ```

  1. 声明变量必须要有关键字
  2. 无法使用`delete`
  3. 无法使用一些未来铺垫的关键字作为变量implements`、`interface`、`let`、`package
  4. 对象操作会更严格,例如只读属性被修改会报错
  5. 函数参数不能重名
  6. 函数中arguments无法被修改
  7. arguments和参数不再互相绑定
  8. 函数声明必须在顶层
  9. 禁止使用eval()
  10. 禁止使用with()
  11. this不会指向全局,函数执行上下文,普通函数
  12. 禁止八进制写法

- .除了加法且一方为字符串,其余减、乘、除、求余基本类型转number,引用类型转valueOf().toString()  所以Number(null) ->0 Number(undefined) -> NaN,1+[] -> 1

- 两边都会转为Number Number([]) -> 0  Number({})

- Function instanceof Object  ,  Object instanceof Function

- 无论同步操作多久,都优先高于微任务和宏任务

- javascript 分为预处理和执行阶段,尽管 a = 2 没有执行 但作用域里的a已经声明了

  ```
  var a = 1;
  function test() {
      console.log(a);
      if(false) {
          var a = 2;
      }
  }
  test();
  ```

- 静态语言 既强类型语言 c, c++, java ,动态语言 既弱类型语言 js

- parseInt("1a") === 1  true

- ie 中 attachEvent 等于其他浏览器的 addEventListener

- 0/0会返回NaN 不会触发catch

- Date setMonth(0~11)  setDate(40) 大于30或31 会进入下一个月

- requestAnimationFrame 非同步执行 所以和循环输出 var i结果一样

- with 改变作用域里的变量,如果没有就会往外泄露,直到全局

- readonly 对button无效,用于表单

- call,bind ,apply 如果传null或者undefined ,this指向全局对象,非严格模式下

- new Boolean(false) ->Boolean {false} 得到一个对象,但是document.write又为结果值,fuck Boolean(false) -> false 得到布尔值,document传的如果不为基本数据类型,会执行toString()

- var foo = new Function('x', 'y', 'return x + y') new Function 可将字符串转为函数

- let num = (function(x){delete x;return x;})(1); 可以从立即执行函数中获取值

- 什么是闭包

  - 内部的函数存在外部作用域的引用就会导致闭包
  - 函数的上级作用域在哪里创建创建的，上级作用域就是谁,是创建的位置而非调用的位置
  - 闭包中的变量存储的位置是堆内存。栈内存有回收机制,如果在栈就被回收了
  - 闭包中的变量是独立的,多个闭包互不干扰
  - 形成的原理：作用域链，当前作用域可以访问上级作用域中的变量

- isNaN  `isNaN`函数会首先尝试将这个参数转换为数值，然后才会对转换后的结果是否是[`NaN`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/NaN)进行判断

- 函数没有重载!!同名函数会覆盖,并且提升

- 数组改变自身的方法,sort也改变了,改变了顺序,concat没改变,返回连接后的副本

- dom id,className innerHTML都是可读可写,tagName 只能读

- continue会跳过后面的内容直接执行 

- 什么是Promise

  - es6新增的构造函数,异步编程的解决方案
  - 有三种状态 pending,fulfilled(Resolved),rejected

- 什么是BFC

  - 从翻译上来说,Block Formatting Context块级格式化上下文,独立的渲染区域、不会影响边界以外的元素,当外边距或者内边距合并时,就可以用BFC解决这个问题
  - 布局规则 1.内部盒子会在垂直方向，一个接一个地放置。2.垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生重叠3.计算BFC的高度时，浮动元素也参与计算
  - float `设置成 `left `或 `right` -`position `是`absolute`或者`fixed` -`overflow `不是`visible`，为 `auto`、`scroll`、`hidden` -`display`是`flex`或者`inline-block
  - 解决问题,清楚浮动

- iframe

  - 创建比一般的 DOM 元素慢了 1-2 个数量级
  - 阻塞页面加载.window 的 onload 事件需要在所有 iframe 加载完毕后（包含里面的元素）才会触发。
  - 唯一的连接池 占用连接池阻塞了主页面资源的加载
  - 不利于 SEO 搜索引擎的检索程序无法解读 iframe另外，iframe 本身不是动态语言，样式和脚本都需要额外导入

- for(;i<6,j<10;) 多个条件判断逗号分隔,以后者为据

- confirm() 确认框 alert()警示框 prompt()对话框 open()打开新窗口

- Object.is() 严格判断是否相等,基本与===一致 除了 +0===-0 ,NaN === NaN 刚好结果相反

- 连等操作是右向左执行的,所以 let a = b= 10 相当于  b = 10 ,let a = b 那么这个b会发生内存溢出

- 只要不写关键字的声明都会泄露到全局 ,当然要注意是没写关键字还是在进行赋值

- let a = {n:1}  let b = a  a.x  = a = {n:2} 点运算符优先级比较高 所以此时先拿到a.x的内存地址,既原来{n:1,x:undefined}

- es6 之前的遍历会自动跳过 undefined 的位置,[0,1,undefined,3]->0,1,3 for of 等es6之后的不会,map会保留

- 非字符串作key,将会调用toString()方法

- const func = (inner.func, inner.func) = inner.func = inner.func ,逗号操作符会返回表达式最后一个值,为函数本身,func,赋值表达式同理,也是返回函数的本身

- Object.assign([1, 2, 3], [4, 5]) ->[4,5,3] 覆盖位置上的值

- typeof NULL 此时NULL为未声明的变量,即为 undefined ,class {} 为es6新增的语法糖,本质上还是一个函数

- 变量和函数同时提升,既名字相同时,忽略变量,有赋值,赋值为准

- 对象->原型对象  读取时,按照原型链读取,修改时1层点都是在对象本身操作,两层点对象原型都没有就报错,原型上有就修改原型上的

- 原始数据类型不包括引用数据类型

- js 烧脑面试大赏[js烧脑面试题大赏 - 掘金 (juejin.cn)](https://juejin.cn/post/6989433079760683022#heading-0)

- class this.变量与getter 变量相同且无set时,变量为只读,修改会报错

- ({} + 'b' > {} + 'a') b的ascii 码比较大

- try-> catch ->finally 如果有finally 那么 try中的return不会直接跳出函数,而是会进入finally,但是finally 执行完之后还是会return 除非break

- break + 标签代码块,跳出代码块,如果try后又finally 在finally之前break try仍然会进入finally

- 类中的静态方法和非静态方法是可以重名的,因为调用者不同,不会出现歧义

- ```
  function bar() {
    return {
      name: 'clc',
      run: () => {
        console.log(this); // 'why' this为bar中的变量,既闭包,因为是箭头函数,就跟调用者无关了,而是看保存的是哪个闭包变量
      }
    }
  }
  
  function bar() {
    return {
      name: 'clc',
      run() {
        console.log(this); // 'clc'
      }
    }
  }
  
  bar.call({ name: 'why' }).run()
  ```

- window.addEventListener(``"click"``, button.change) 此时button.change不再是调用者了,这里不是执行,执行由window决定

- 不要在块内声明一个函数(use strict) 会报错,如果需要这么做,使用函数表达式来声明(命令声明,函数表达式声明,构造函数声明)

- new 关键字 如果手动返回了引用类型 则该引用类型替换自动生成的,如果是基本类型,则仍然是由new 内部生成的对象决定

- 创建->初始化->赋值  变量提升,let var const 都会提升,此时决定使用内部的还是外部的变量,但是var 会先初始化为 undefined,let const 不会,存在暂时性死区

- addEventListener  第三个参数默认为false 决定是否在捕获的时候触发,默认冒泡的时候触发

- [JavaScript实现继承的6种方式 - Leophen - 博客园 (cnblogs.com)](https://www.cnblogs.com/Leophen/p/11401734.html)原型链,构造函数,组合,原型式,寄生式,寄生组合式.

  - 原型链  一个构造函数的原型是另一个类型的实例
    - 创建子类时不能往超类传递数据
    - 所有子类的实例的原型都指向同一个父类的实例,所有父类实例上的引用类型再子类实例都是共享的
  - 构造函数式 在子类型构造函数的内部调用父类型构造函数通过call或者bind绑定this,相当于都在自身进行
    - 引用类型不共享了,但是父类函数方法也不能复用了
    - 访问不到父类原型 (没有关联)
  - 组合式 (原型链+构造函数式)最常见的方法 可传递数据到父类,引用数据在自身不共享,方法在父类原型上
    - 是会调用两次父类构造函数
  - 原型式 Object.create
    -  (const foo = Object.create({ name: 'clc',age:19}, { age: { value: 18} });)  function object(o){function F(){} F.prototype = o;return new F();} 第一个参数为创建出的新对象的隐式原型 ,第二个参数如果第一个参数有同名则覆盖,无则为foo自身的属性
    -  缺点同原型链

  - 寄生式 函数封装 增强了object.create,还是做不到复用
  - 寄生组合式
    - 减少了组合式中的一次父类原型生成

- console.log.call(console,this); 函数内的调用this的指向为console,但打印的this为外部传进去的window

- undefined 和null 和任意有意义的值相比 (==) 都返回false ,但null ==undefined 之间为true null == false false

- 'Value is ' + (val != '0') ? 'define' : 'undefine' -> define 因为加号运算符优先级大于?

- var foo = function bar() {}; 此时的bar 作为foo.name 并不是函数bar

- 未使用关键字还有eval()创建的变量可以被delete 删除

- 不支持冒泡 mouseenter mouseleave load unload resize focus blur

- 匿名函数的length 为形参个数,

- var str = "Hellllo world";  str = str.replace(/(l)\1/g, '$1');  \1何$1都为第一个分组

- js 判断类型

  - typeof
  - constructor
  - instanceof
  - Object.prototype.toString.call()

- 说一说样式优先级的规则

  - !important
  - 引入方式,行内大于嵌入和外链 嵌入和外链看引入顺序,后者覆盖前者
  - 选择器的优先级 id选择器>（类选择器 | 伪类选择器 | 属性选择器 ）> （后代选择器 | 伪元素选择器 ）> （子选择器 | 相邻选择器） > 通配符选择器 
  - 继承样式
  - 浏览器默认样式


- js 实现异步的方式 .所有异步任务都是在同步任务执行结束之后，从任务队列中依次取出执行
  - 回调函数 比如AJAX回调 ,简单容易实现,不利于阅读和维护,高度耦合,结构混乱,流程难以追踪
  - 事件监听
  - setTimeOut
  - Promise 能够捕获错误,很好的解决地狱回调的问题,缺点是无法取消promise
  - 生成器Generators/yield、es6新增的异步编程解决方案,Generator 函数是一个状态机，封装了多个内部状态,可暂停函数, yield可暂停，next方法可启动优点是异步语义清晰，缺点是手动迭代`Generator` 函数很麻烦
  - async/await 基于Promise实现的 使得异步代码像同步代码 优点是方法清晰不了,缺点是强行使用降低性能
- vue2.0双向绑定的原理与缺陷
  - 响应式指的是：组件的data发生变化，立刻触发视图的更新 
  - Vue 采用数据劫持结合发布者-订阅者模式的方式来实现数据的响应式 Object.defineProperty
  - 缺点 1.一次性递归到底开销很大,当数据很大时大量的递归导致调用栈溢出,因为所有的数据都要进行Obect.de.... 2不能监听新增和删除,数组下标的改变
- vue3.0双向绑定的原理

  - Proxy实现的数据双向绑定
  - 劫持整个对象,弥补了Object.defineProperty 需要迭代遍历,和无法监听新增删除,数组下标的缺陷
- 数组的去重有哪些方法
  - 新数组存储只出现过一次的元素 占用空间大
  - [...new Set(arr)]
  - filter +indexof index 相同即为第一个
- null 和undefined 的区别
  - undefined 变量没有赋值, 函数没有返回值,对象不存在的属性,有形参无实参即为undefiend,
  - null  定义了且赋值为nullo,人为设置的空对象,释放对象 直接赋值为null
- 浮动
  - 让元素脱离文档流,实现图片文字环绕效果
  - 浮动块级元素可排列在同一行
  - 缺点,父元素高度塌陷,影响其他元素排版,清除浮动,给父元素加上 .clearfix::after { content: ''; display: table; clear: both; } ,bfc
- 箭头函数
  - 箭头函数相当于匿名函数，简化了函数定义。
  - 没有this,this从外部继承,单条语句可忽略return和{}
  - 没有this,不能作为构造函数 ,当使用call,bind,apply时无法绑定this
  - 没有原型和super不能使用yield关键字，因此箭头函数不能用作 Generator 函数。\
- this指向
  - 全局执行上下文 无论是否严格模式 都指向全局对象
  - 函数执行上下文 严格模式 普通函数为undefined ,非严格为全局对象 箭头函数都顺着作用域链外上找
- css 设置尺寸的单位
  - px ,em,vw,vh,rem
- 水平垂直居中方法
  - 行盒 text-align vertical-align
  - 块盒 justifly-content align-items 
  - position:absolute;left:50%;right:50% transform: translate(-50%,-50%);
- js变量的提升,
  - var 提升   定义 初始化 赋值
  - const let 不提升 暂时性死区
  - 函数声明提升
- HashRouter 和 HistoryRouter的区别和原理
  - history和hash都是利用浏览器的两种特性实现前端路由
  - history浏览历史记录栈的API,没有 # 需要后端配合,否则刷新404 history.pushState replaceState 进行页面跳转,window.onpopstate监听,更优雅
  - hash 监听location对象hash值变化,window.onhashchange ,兼容性更好
- Node在执行微任务的时候会优先执行process.nextTick() , promise.then() 
- Object(1)||new Object(1)  == new Number(1)  传字符串 为 String 对象
- ^\[abc\]\[1,2]$ 匹配 a1 a2 b1 b2 c1 c2这里[]中的逗号仅作分隔使用
- 什么是XML

  - XML 指可扩展标记语言（**EXtensible Markup Language**）
  - XML 是一种标记语言，很类似 HTML
  - XML 的设计宗旨是传输数据，而非显示数据
  - XML 标签没有被预定义。您需要自行定义标签。
  - XML 被设计为具有自我描述性。
  - XML 是 W3C 的推荐标准
- XML 与 HTML 的主要差异

  - XML 不是 HTML 的替代。
  - XML 和 HTML 为不同的目的而设计：
  - XML 被设计为传输和存储数据，其焦点是数据的内容。
  - HTML 被设计用来显示数据，其焦点是数据的外观。
  - HTML 旨在显示信息，而 XML 旨在传输信息。
- 类的声明同let 和const 有暂时性死区
- typeof [] 为 object 只有函数为function
- 函数传参,时相当于创建了一个变量,并且赋值,和下面的同名变量都提升了
- 浏览器不兼容CommonJS的根本原因，在于缺少四个Node.js环境的变量。 module exports require global 
- Symbol.for() 和Symbol()不同的时,他会将创建的Symbol()放入到一个全局的注册表中,如果已有相同的key,返回已存在注册表的Symbol()
- Symbol 值不可以和其他类型值进行混合运算,否则会报错
- 基本类型占用8byte 64位
- js 内置的可迭代对象 Array Map Set String TypedArray Arguments NodeList
- slice() 截取数组并且返回新数组
- f = (x = xxxxx) => x; f(2) √ f() error 有实参,忽略默认值,读取默认值报错
- es5 forEach() filter() reduce() every() some()若数组有undefined 都会跳过空位,且不保留 只有map会保留undefined 值
- RegExp 的方法 test exec compile(已弃用)
- IIFE 立即执行函数 + NFE 具名函数 的函数名为常量 不可修改,此时的函数名变量为局部变量,不是全局函数,函数名a 和形参a 形参的优先级高
- *函数提升优先级高于变量提升*,且不会被同名变量声明时覆盖,但是会被变量赋值后覆盖
- eval 会返回最后一个表达式的结果
- 2.toString() error 数字后面直接跟小数点会被解析为小数
- repaint 重绘

  - 文字颜色
  - 背景颜色
- reflow 回流

  - 改变窗口大小
  - 改变文字大小
  - 内容的改变,输入框输入
  - 激活伪类,hover
  - 操作class 属性
  - 脚本操作DOM
  - 计算offsetWidth offsetHeight scrollTop等属性,浏览器都会重排获取最新的值
  - 计算style属性
- 说一下重绘、回流/重排区别如何避免？ 当元素发生几何变化,位置大小尺寸,那么就会发生回流/重排,重排一定重绘,而改变颜色只会重绘,跳过了render 和分层分块的步骤,重绘是不怎么消耗性能的,所以要注重的是重排,

  - 样式一次性集中改变
  - position 脱离文档流
  - 使用GPU加速
- Event Loop 执行js代码时，遇见同步任务，直接推入调用栈执行，遇到异步任务，将该任务挂起，等到异步任务有返回之后推入到任务队列中，当调用栈中的所有同步任务全部执行完成，将任务队列中的任务按顺序一个一个的推入并执行，重复执行这一系列的行为。浏览器和Node 环境下，microtask 任务队列的执行时机不同 - Node端，microtask 在事件循环的各个阶段之间执行 - 浏览器端，microtask 在事件循环的 macrotask 执行完之后执行
- 宏任务(macrotask) 执行script标签内部代码、setTimeout/setInterval、ajax、postMessageMessageChannel、setImmediate(异步的尽可能块,大部分情况比timeout 0优先,但不是绝对的执行顺序取决于各种因素,在事件循环的下一个迭代中执行)，I/O（Node.js）
- 微任务(microtask ) Promise、MutonObserver、Object.observe、process.nextTick（Node.js）
- 说一下diff 算法(patch ,pathchVnode updateChildren)

  - vue 和 react  组件渲染的时候会返回virtual dom,渲染器再把vdom 通过增删改的api同步到dom,再次渲染的时候产生新的vdom 新旧vdom之间的对比找到差异的算法就是diff算法
  - 树的对比是O(n\*3) ,多对多为 n\*2,插入,删除,修改也为n的复杂度,所以约定只做同层对比,type类型改变的子节点不对比,dom记录了关联节点,增删改也不遍历,如此 On3变成On
  - 对比一次,复杂度大幅降低,但是处理调换顺序的时候不智能了,顺序一改变导致节点和子节点都要重新渲染,时间复杂度降低了,dom的操作次数增加,所以需要key
  - 简单diff :找相同的key,有的话移动按照新vdom的顺序调换,没有的话执行插入,锚点是上一个节点的nextSibling
  - 双端diff:4个指针同时指向新旧vdom的头尾,patch函数比较新老,不存在创建,多了销毁,相同则进入patchVnode,在进行三种children的情况判断,新增删除,对比,执行updateChildren 如果children 是textNode 直接更新文本,否则进行头头,尾尾,头尾,尾头对比
- 三栏布局

  - 圣杯布局 两边盒子宽度固定 中间盒子自适应的三栏布局 ,三栏float left ,父元素padding, left right 设置负的margin 和left right 移动到padding处
  - 双飞翼布局 同圣杯 区别于父元素padding 变成中间元素的margin ,缺点多套了一层dom,优点在于对比圣杯,不要设置min-body也不会变形
- 浏览器垃圾回收机制

  - 根据数据的存储方式也就是数据类型分为 堆回收和栈垃圾回收

    - 栈垃圾回收 例如一个函数执行完 ,js 上下移动ESP销毁上下文,根据后入先进的原则销毁

  - 可达性 从根节点出发(window,dom树 栈上的变量)遍历所有的对象,可以遍历到的对象就是可达的
  - 内存碎片 当不可达对象被回收以后,内存中会出现大量的不连续空间
  - 长久对象(老生代) 声明周期很长的对象,比如window/Dom
  - 临时对象(新生代) 函数内部,块级作用域变量对象
  - 主垃圾回收器(标记清除算法) 运用优化版的可达性算法标记可达的对象,回收后出现内存碎片,再进行内存整理
  - 副垃圾回收器(Scavenge算法) 大概支持1~8 M的容量,分为两个区域 对象区域和空闲区域,新回收的副垃圾进入对象区域,等块存满的时候执行一次垃圾清理,清理过程为

    - 标记所有对象区域的垃圾对象
    - 把对象区域的对象移动到空闲区域排列好
    - 把空闲区域和对象区域对调(其实就是两个对象区域) 如此排列清理就不会出现内存碎片的问题

  - 增量回收  浏览器在进行垃圾回收的时候，会暂停JS脚本，可能会导致卡顿.增量回收将垃圾回收工作分成很小的块,与js代码循环多次处理,避免卡顿
  - 闲时收集 垃圾收集器只在cpu空闲时尝试运行,
  - 内存泄露 无法被垃圾回收机制回收

    - window 事件没有解绑
    - vue 中watch之后没有unwatch
    - 互相引用,
    - 定时器
    - 滥用闭包
- 说一说 vue 的keep-alive 组件 vue用来缓存组件的内置组件,提升性能通常是用来缓存路由. 有两个属性 include exclude ,通常用于路由
- 1<2<3 连续关系运算符  2>1 true -> 1 3>1 true 
- 什么是CSRF (cross site request forgey) 攻击者盗用了你的身份，以你的名义发送恶意请求，对服务器来说这个请求是完全合法的

  - 登陆受信任网站A,并在本地生成Cookie

  - 在不登出A的情况下,访问危险网站B

  - B收到用户请求之后返回一些攻击代码.要求访问返回cookie的网站A就是以用户的角度访问了网站A
  - 预防CSRF策略

    - 验证码 要求用户与应用之间进行交互
    - HTTP request header 中的 referer 检查是否是当前域名过来,并不是万无一失的,refer由浏览器生成,跟浏览器的漏洞安全有关
    - token 验证 在get 或者post 添加与后端token检验 但是get或者post传参的不便性。也不是绝对安全
    - 把token放在自定义的请求头中,自定义的不会记录在浏览器的地址栏上
- 什么是XSS (cross site scripting) 区分css 改为xss.攻击者向Web页面里面插入script代码,当用户浏览这个页面的时候,就会运行攻击者插入的代码

  - 反射型  攻击者构造出特殊的 URL，其中包含恶意代码。用户打开URL 时，网站服务端将HTML和恶意代码都返回给浏览器。浏览器解析html,且执行恶意代码,窃取用户数据,冒充用户行为.常见于网站搜索,挑战等
  - 存储型 攻击者把恶意代码提交到网站的数据库上.用户在解析html时,也解析了存储在数据库的恶意代码.常见于论坛发帖、商品评论、用户私信等。
  - 防止XSS

    - 对用户数据进行严格的编码HTML元素的编码，JavaScript编码，css编码，url编码等
    - html代码 转义<,>
    - js 代码序列化,
    - Http Only cookie 无法从document.cookie获取cookie
- 浏览器是如何渲染页面的  将 html -> dom树,将css ->stylesheet,根据dom树和stylesheet结合生成渲染树render tree,将渲染树进行分层,为每一层绘制列表,再把每一层分成图块,紧接着光栅化将图块绘制成位图,最后所有位图合成为一个页面  

  - 分层的目的,当某一层有动画时,避免整个图层渲染,
  - 光栅化,分块的目的 只渲染可视的附近区域
- computed 和watch 的区别

  - computed 有缓存,依赖属性变化
  - watch 无缓存,支持异步,监听数据变化
- 说一说 Vue 中 $nextTick 作用与原理? Vue的响应式是异步的,当数据发生改变的时候,视图不会立刻更新,而是将同一事件循环的所有数据变化完成以后统一更新,所以在修改dom之后,立刻获取dom,或者修改props,此时的还是未修改的,  $nextTick本质上是返回一个promise,他会在当前事件执行完成以后再执行,.
- token 能放在cookie中吗 ,当然,token就是用来判断用户是否登录的,通常里面包含用户的唯一标识,uid ,时间戳 time 签名 sign.token 是否过期应该由后端来判断,当token失效的时候返回状态码401  用户登录,服务的返回token前端存储token再cookie,每一次发送请求都携带token,服务端验证token
- 浏览器输入url发生了什么

  1. url解析 判断是搜索内容还是请求url
  2. 查找缓存 浏览器查看浏览器缓存,系统缓存,路由缓存,ISP缓存
  3. DNS解析 浏览器向DNS服务器发起请求,解析URL域名对应的IP地址(DNS服务器是基于UDP协议)
  4. 建立TCP连接 解析出IP地址后,根据默认端口80 和服务器建立TCP连接
  5. 发起HTTP请求 浏览器发起读取文件的HTTP请求,该请求报文会作为TCP连接的第三次握手数据发送给服务器
  6. 服务器响应请求有重定向返回重定向,浏览器再根据重定向发起请求,如果请求参数有误返回404,服务器有问题返回500,一切正常返回200并返回html
  7. 关闭TCP连接 通过四次挥手后释放TCP连接
  8. 浏览器解析HTML并渲染
- 浏览器的缓存机制 

  - 浏览器每次发起请求,都会现在浏览器的缓存中查找结果和缓存标识(第一次发起请求默认为no-cache,所以第二次会发送 max-age=0 private 即为进入协商缓存)
  - 浏览器每次拿到结果都会将结果和缓存标识存到浏览器缓存中
  - 强制缓存 有强制缓存且仍在有效期 直接返回,不在有效期,进入协商缓存,向服务器发起请求并携带缓存标识
    - Cache-Control  http/1.1 缓存字段 优先级更高,值为
      - public：所有内容都将被缓存（客户端和代理服务器都可缓存）
      - private：所有内容只有客户端可以缓存，Cache-Control的默认取值
      - no-cache：客户端缓存内容，但是是否使用缓存则需要经过协商缓存来验证决定
      - no-store：所有内容都不会被缓存，即不使用强制缓存，也不使用协商缓存
      - max-age=xxx (xxx is numeric)：缓存内容将在xxx秒后失效,原服务器 以这个值为准
      - s-maxage=xxx 代理服务器的缓存时间
    - expires http/1.0的缓存字段,值为到期时间,与客户端时间进行判断,容易修改,时区不同,误差比较大,淘汰
  - 协商缓存 在有效期返回304 ,使用缓存 ,不在有效期 返回200 和请求结果
    - Etag / If-None-Match 优先级更高 值为哈希值/唯一标识/指纹码
    - Last-Modified / If-Modified-Since Last-Modified是服务器响应请求时，返回该资源文件在服务器最后被修改的时间， If-Modified-Since 为上一次请求时Last-Modified的值,比较二者相同返回304
  - from memory cache  内存中的缓存 读取顺序为memory->disk
  - from disk cache 硬盘中的缓存
- 304的过程 304 Not Modified 请求的资源为改变
  - 验证 Cache-Control/Expire 是否有强缓存 是否过期
  - 验证etag/If-None-Match Last-Modified / If-Modified-Sinc 验证协商缓存是否过期
- TCP的三次握手

  - 第一次握手 客户端发送SYN标志和序号  (SYN=1,seq = x)
  - 第二次握手 服务器收到SYN包并且确认,同时也发送一个自己的SYN包,即SYN+ACK包( SYN=1,ACK=1,seq = y,ack=x+1)
  - 第三次握手 客户端收到SYN+ACK包,向服务器发送确认包和序号(ACK = 1,ack = y+1,seq=x+1+1)

  - 客户端的状态 close -> syn_sent(发送状态) ->Estab-lished(稳定连接)
  - 服务端状态 close -> syn_recvd(回复) -> Estab-lished(稳定连接)
  - 序号(seq) 32位，用来标识从TCP源端向目的端发送的字节流
  - 确认号(ack) 32位，只有ACK标志位为1时，确认序号字段才有效，ack=seq+1。
  - 标志位(Flag)
    - URG：紧急指针（urgent pointer）有效。
    - ACK：确认序号有效。（为了与**确认号ack**区分开，我们用大写表示）
    - PSH：接收方应该尽快将这个报文交给应用层。
    - RST：重置连接。
    - SYN：发起一个新连接。(同步序列编号)
    - FIN：释放一个连接。
  - TCP握手过程中 ack和seq 都是在批次的ack和seq之间计算,确保TCP的连贯性
- 为什么要进行三次握手

  - 减小服务器开销.为了防止服务器端开启一些无用的连接增加服务器开销(一开始服务器都保持close状态)
  - 接收到失效请求发生的错误.防止已失效的连接请求报文段突然又传送到了服务端，因而产生错误。
- TCP的四次挥手

  - 第一次挥手 客户端发送 FIN标志和序号 (FIN = 1,seq = u) 
  - 第二次挥手 服务端接受并返回 ACK标志,序号和确认号 ( ACK = 1,seq = v,ack=u+1)
  - 第三次挥手 服务器再次发出标志位FIN,ACK(表示已经准备好释放连接,此处ACK非确认标识)  ( ACK = 1,FIN = 1,seq = w, ack=u+1)
  - 第四次挥手 客户端发出 ACK,seq = u+1 ,ack =w +1 随后客户端开始在TIME-WAIT阶段等待2MSL
  - 客户端的状态 Estab-lished ->FIN-WAIT-1终止等待1 -> FIN-WAIT-2终止等待2 ->TIME-WATI 时间等待 ->close
  - 服务端的状态 Estab-lished ->CLOSE-WAIT 关闭等待 -> LAST-ACK 最后确认 ->close
- 为什么要四次挥手 .因为第二次握手,服务器同时返回了SYN和ACK标志,而挥手的标志ACK和FIN分别为第二第三次挥手传送,因为握手时,服务端不需要任何准备,而挥手,服务端需要释放一些数据,所以才需要CLOSE-WAIT和LAST-ACK两个阶段
- 为什么客户端在TIME-WAIT阶段要等两**2MSL** , 为的是确认服务器收到第四次挥手的ACK包, 因为服务端在第三次挥手时,如果在1MSL内没有收到客户端发出的ACK确认报文，就会再次向客户端发出FIN报文.所以如果在客户端2MSL再次接收到FIN包,证明了服务端未收到第四次挥手的ACK包,那么客户端会再次发送并且定时器重置.否则为服务端接收到了ACK包,客户端进入CLOSE状态,比服务端晚.所以挥手是最少四次
- 组件通信方式

  - 父子通信 props emit proview injectg
  - 其他通信 EventBus,vuex
- 说一说盒模型 ,决定一个盒子的大小由margin padding border content,标准盒width/height 设置的是content,怪异盒设置的是padding+border+content
- 伪数组和数组的区别  都有length属性,都可以用for in  ,一个是array 一个本质是object  可以用数组的call方法,Array.from将伪数组转为真数组
- expire localstorage
  - 惰性删除 下次使用的时,检查expire字段
  - 定时删除 设置的时候同时设一个定时器
- axios( Axios 是一个基于 promise 的 HTTP 库)拦截器

  - 请求拦截 添加token,header
  - 响应拦截 校验token ,操作数据
- 创建ajax过程

  - 创建 xhr对象  new XMLHttpRequest() 
  - 设置请求参数 xhr.open(Method, 服务器接口地址);
  - 发送请求: request.send(data) post请求需要参数data
  - 监听xhr状态变化 ,XHR.onreadystatechange = function () { if (XHR.readyState == 4 && XHR.status == 200) { console.log(XHR.responseText);
- fetch 请求 fetch是一种HTTP数据请求的方式 是xhr的一种替代方案,它本身就会返回promise
- 前端后实时通信

  - 轮询 实现简单,占用流量,cpu,时间过长无法及时响应,客户端定时发送请求,服务器响应
  - 长轮询  服务器收到响应后,若无数据则等待直到超时再返回,客户端收到返回结果后再次发送请求
  - iframe流 frame流方式是在页面中插入一个隐藏的iframe，利用其src属性在服务器和客户端之间创建一条长连接，服务器向iframe传输数据 维护一个长连接会增加开销
  - websocket
  - SSE  SSE(Server-Sent Event)是建立在浏览器与服务器之间的通信渠道，然后服务器向浏览器推送信息。SSE 是单向通道，只能服务器向浏览器发送
- Vue 为什么要加key 为了性能优化,因为更新dom是需要用diff算法进行对比,如果没有手动传入key那么会使用index做key,当交换顺序的时候,所有的元素就需要重新渲染,有了key之后则key相同的元素不需要重新渲染
- vuerouter 懒加载的方法 

  - component: resolve=>(require(['../views/About'],resolve))   require 手动返回 promise
  - component: () => import(/* webpackChunkName: "about" */ '../views/About.vue') import 返回的就是promise
- 事件拓展符的用法

  - spread syntax 展开对象,展开数组
  - rest syntax 剩余 凝聚成数组
- 说一说服务端渲染 减少网络传输，响应快，用户体验好，首屏渲染快，对搜索引擎友好，搜索引擎爬虫可以看到完整的程序源码，有利于SEO。
- 前端优化手段 [前端性能优化 24 条建议（2020） - 掘金 (juejin.cn)](https://juejin.cn/post/6892994632968306702#heading-19)

  - 加载更快

    - 减小加载文件大小: 压缩文件,图片
    - 减少加载次数 : 雪碧图,节流防抖
  - 渲染更快

    - 提前渲染 ssr,css放在header ,js放在body 避免渲染阻塞,懒加载,
    - 合并渲染操作,避免回流
  - 减少,减小http请求
  - 使用http2
  - 使用ssr服务端渲染
  - 使用cdn
  - 先执行css在执行js
  - 使用字体图标替代图片
  - 缓存策略
  - 压缩文件
  - 图片优化
  - 按需加载
  - 减少回流
  - 事件委托
  - 使用requestAnimationFrame 替代 set
  - 算法
- 性能优化有哪些性能指标,如何量化

  - FCP（First Contentful Paint）首次内容绘制 指浏览器从响应用户输入网络地址到页面内容的任何部分在屏幕上完成渲染的时间。这个就是实际有意义的首屏时间。
  - LCP（Largest Contentful Paint）最大内容绘制 表示可视区最大内容（文本块或图像元素）在屏幕上完成渲染的时间。该时间会随着页面渲染变化而变化，因为页面中的最大元素在渲染过程中可能会发生改变，另外该指标会在用户第一次交互后停止记录。
  - TTI（Time to Interactive）可交互时间 测量页面从开始加载到视觉上完成渲染、初始脚本完成加载，并能够快速、可靠地响应用户输入所需的可交互状态时间。 可交互状态指的是页面上的 UI 组件是可以交互的（可以响应按钮的点击或在文本框输入文字等）。
  - TBT（Total Blocking Time）总阻塞时间 FCP+TTI 
  - CLS (Cumulative Layout Shift) 累积布局偏移 每当一个可见元素的位置从一个已渲染帧变更到下一个已渲染帧时，就发生了布局偏移 。
  - FID（First input delay）首次输入延迟 用户单击链接、点按按钮或使用由JavaScript驱动的自定义控件）直到浏览器实际能够对交互做出响应所经过的时间
  - 
- 前端监控

  - 数据监控(监控用户行为)
  
  - 性能监控(监控页面性能)
  
  - 异常监控(监控产品,系统异常)
  
- 前端异常监控

  - 发生了什么错误
  - 时间段
  - 影响了多少用户
  - 哪些页面
  - 错误的原因
  - 定位解决问题
  - app.config.errorHandler    vue的错误监控
  - window.onerror     脚本错误
  - window.addEventListener( 'unhandledrejection')   promise 未捕获异常
  - window.addEventListener( 'error')    静态资源加载错误
  - 搜集上报 -> 采集聚合 -> 可视化分析  -> 监控告警
- 为什么要开启GZIP,减少css,js,html,xml的传输大小,但是需要消耗cpu去解压,有利有弊要平衡,压缩率为原来的30%,不建议压缩图片和大文件,图片本身就有压缩,大文件消耗CPU得不偿失

  - gzip两种方案(对应的nginx conf配置不一样)

    - 在线解压 
    - 本地解压 
  - Content-Encoding值

    - gzip 表明实体采用GNU zip编码（使用最多）
    - compress 表明实体采用Unix的文件压缩程序
    - deflate　表明实体是用zlib的格式压缩的
    - identity　表明没有对实体进行编码。当没有Content-Encoding header时， 就默认为这种情况
  - Accept-Encoding值

    - gzip
    - compress
    - deflate
    - br 　　 一种新的压缩算法 Brotli
- http

  - 服务器传输超文本到本地浏览器的超文本传输协议.信息是明文
  - 默认端口80
  - 无状态连接
- https

  - http下加入 SSL 证书层进行加密 确保数据传输,确保网站真实,防止数据在传输过程中被窃
  - 默认端口443
  - 握手比较费时,加载时间,耗电增加
  - 缓存不如http高效,增加数据开销
  - 需要ca证书,功能越强大的越高
  - ssl证书需要绑定ip
- https协议工作原理

  - 客户端请求https url ,建立ssl链接
  - 服务器收到请求之后返回网站证书(证书中包含了公钥)给客户端
  - 客户端和服务端协商ssl链接的安全等级/加密等级
  - 协商一致的安全等级以后,建立会话密钥,客户端通过公钥来加密会话密钥
  - 服务端通过私钥解密出会话密钥
  - 服务端再通过会话密钥与客户端之前进行通信
- 什么是mvvm


  - mvc model view controller  操作dom更新视图
  - mvvm model view  viewmodel  数据驱动视图
  - 优点

    - 低耦合一个model 可以绑定到多个view 上  view改变不一定改变model ,model 改变view也可以不变
    - 可重复 封装
    - 独立开发  更专注于某一个块开发
    - 可测试

- webpack的优化


  - 优化构建速度
  - 优化打包体积

    - 压缩代码
    - 提取公共资源
    - tree shaking  移除未使用的代码
    - Scope hoisting 将所有模块的代码按照引用顺序放在⼀个函数作用域，然后适当的重命名⼀些变量以防止变量名冲突。
    - 图片压缩
    - 动态polyfill

- babel 的编译过程


  - babel 本质是一个js的编译器,将es5以后的代码转换为向后兼容的js
  - babel 本质就是才操作ast(抽象语法树)来完成代码的编译
  - 解析  将源代码转换成更加抽象的表示方法（例如抽象语法树）。包括词法分析和语法分析。词法分析主要把字符流源代码（Char Stream）转换成令牌流（ Token Stream），语法分析主要是将令牌流转换成抽象语法树（Abstract Syntax Tree，AST）。
  - 转换 通过 Babel 的插件能力，对（抽象语法树）做一些特殊处理，将高版本语法的 AST 转换成支持低版本语法的 AST。让它符合编译器的期望，当然在此过程中也可以对 AST 的 Node 节点进行优化操作，比如添加、更新以及移除节点等
  - 生成  将 AST 转换成字符串形式的低版本代码，同时也能创建 Source Map 映射。
  - await 后的执行代码相当于promise.then 也在微任务中 ,若无reslove 则不执行
  - require('xxx') 查找包过程

    - 首先找到 package.json 同级的 node_modules 
    - 找到'xxx' 包
    - 找到'xxx'下的package.json 的main 字段中的js文件
    - 若没有package.json或没有 main字段 则默认加载'xxx' 包的index.js 文件
    - 若没有则查找上一级的node_modules 直到根目录,最后报错

 - 判断链表是否有环

   - 哈希表 set 遍历存储判断
   - 遍历链表添加访问字段
   - 快慢指针,若追上则为环

 - Vue.use 原理  链式调用每一次

   ```javascript
   Vue.use = function (plugin) {
       const installedPlugins = (this._installedPlugins || (this._installedPlugins = []))
       if (installedPlugins.indexOf(plugin) > -1) {
           return this
       }
    
       // additional parameters
       const args = toArray(arguments, 1)
       args.unshift(this)
       if (typeof plugin.install === 'function') {
           plugin.install.apply(plugin, args)
       } else if (typeof plugin === 'function') {
           plugin.apply(null, args)
       }
       installedPlugins.push(plugin)
       return this
   }
   // 每一次都返回this链式调用
   // 获取Vue身上的_installedPlugins 判断是否已经安装过
   // 如果plugin是对象则执行他身上的install方法,如果是function 则直接执行
   ```

 - js 实现异步任务调度器

   ```
   const sleep = time => new Promise(resolve => setTimeout(resolve, time));
   
   class Scheduler {
     constructor(max) {
       this.max = max;
       this.count = 0;
       this.queue = [];
     }
   
     async add(fn) {
   
       if (this.count >= this.max) {
         await new Promise(resolve => this.queue.push(resolve));
       }
   
       this.count++;
       const res = await fn();
       this.count--;
       this.queue.length && this.queue.shift()();
       return res;
     }
   }
   
   
   const scheduler = new Scheduler(1);
   
   const addTask = (time, val) => {
     scheduler.add(() => sleep(time)).then(() => console.log(val))
   };
   
   addTask(1000, '1');
   addTask(1000, '2');
   addTask(1000, '3');
   addTask(1000, '4');
   ```

   ```
   const sleep = delayInms => new Promise(resolve => setTimeout(resolve, delayInms))
   
   class Scheduler {
     constructor(max) {
       this.max = max
       this.working = []
       this.notWorking = []
     }
   
     addTask(task) {
       return new Promise(resolve => {
         task.resolve = resolve
   
         if (this.working.length < this.max) {
           return this.runTask(task)
         } else {
           this.notWorking.push(task)
         }
       });
     }
   
     runTask(task) {
       this.working.push(task)
   
       return task().then(() => {
         task.resolve()
   
         const index = this.working.indexOf(task)
         this.working.splice(index, 1)
   
         if (this.notWorking.length) {
           this.runTask(this.notWorking.shift())
         }
       })
     }
   }
   
   const scheduler = new Scheduler(1)
   
   async function addTask(delay, value) {
     scheduler.addTask(() => sleep(delay)).then(() => {
       console.log(value);
     })
   }
   
   addTask(2000, '2')
   addTask(1000, '1')
   addTask(1000, '1')
   addTask(1000, '1')
   ```

   
