JavaScript
javascript=ecmascript(european computer manufacturer's association)标准+dom(document object model文档对象模型)+bom(browser object model 浏览器对象模型)
## Function
alert("");  pop up box
document.write("");  write content to body
console.log("");  write to console
从上到下 按顺序执行

书写在属性   结构与行为耦合 
<button onclick="alert('');"></button>
<a href="javascript:;"></a>

引入外部js文件 方便引入,缓存
<script type="text/javascript" src="./clc.js">

script元素引入外部文件后,编写代码无效,可创新标签

//单行注释      /*  多行注释*/``



1.Js 严格区分大小写,
2.每一条语句分号结尾,浏览器会自动添加,有一些浏览器会添加错误
3.JS会忽略多个空行和换行
4.常量,即字面量,不可变  变量,即用来存储字面量方便实用
5.var 声明变量  
6.标识符  字母 数字 下划线 $  不能数字打头
    小驼峰命名法 首字母小写,后面单词开头大写
7.数据类型 
基本数据类型D
String 字符串 Number 数字 Boolean 布尔值 Null 空值 Undefined 未定义 声明了,但没赋值
唯独使用typeof 检查null得到的是object  理解为空的对象
引用数据类型  object 对象 
8 \转义字符 \""
9 typeof 检查数据类型 
10 js有默认的最大 最小正值 Number.MIN_VALUE Number.MAX_VALUE 超过返回infinity  -infinity
11 NaN  not a number   TYPE为number 不要用js计算浮点数,不精准
12 数据类型转换 a=String(a); undefined  sting可以转换   a.toString(); 无法转换null 转换数字可加基数转换 a.toString(2);二进
Number()函数  非纯数字,undefined转为NAN  空串或者空格转换为0  null,false 转换为0 true 为1 011为11,前导0忽略
parseInt();可用于取整 解析,内容不能被阻隔对非string使用会先转换为string  忽略第一个空格,指定基数是很有必要的
 parseFloat();  只解析十进制,第一个小数点有效,不需要指定参数
Boolean(); 除了 NAN和0其余都为true,字符串除了空,其余都是true, null和undefined为false object为true
13.其他进制  16进制 0x  八进制0开头 二进制0b开头,web-kit兼容性不好  当八进制数值超出范围,前缀忽略,2,十六报错 严格模式无效
解决方法 a=parseInt(a,10);防止"070"
14.typeof返回的是字符串
15  a=a+"",把数字a编程字符串a  - 0 *0 /1转 number类型
16 一元操作符,a="123" a=+a;
17a= 1; console(a++); 1 console(++a); 2  a的值,a++表达式的值
18 "use strict";   严格模式 顶部或者函数体添加
19 函数内var 即为局部变量  省略为全局,但不推荐
20 一条语句可声明多个多种类型变量,逗号分隔
21undefined派生自null ecma-262规定了undefined==null返回true
22 console.log() 未声明 报错,未初始化,默认值为undefined,但是typeof 都为Undefined类型
23 浮点数 0.1 =.1   3.145e7 3.145×10的7次方
24 isFinite();在最大和最小值之间返回true
25 NaN不等于它自身 NaN!=NaN,与任何数值运算result为NaNQ
26.console.log(isNaN(NaN));尝试将参数转为数值,可以转换返回false,否则true
27.\r回车,\x41十六进制'A'字符a,\转义多长都视为一个字符
28.!非    对非布尔值进行!先转换为boolean,
&&与 ||或 如果第一个值为false,与不会计算第二个,或同理,遇true停,短路运算符  先转换为布尔类型,返回原值
&& 非布尔运算的返回值1.都为true返回后边的,2.遇到false返回false
|| 1.都为false返回第二个false,遇到true返回true
29关系运算符> < 一边为非数值进行关系运算符将非数值转换为数值,任何值和NAN比较都会false 
    两边都为字符串时,比较unicode编码,ab <ac  先比较a和a再比较后面,有结果出结果
    比较两个字符串型的数字时,切记要转型,不然出现不可预期的错误
29 万国码 unicode js 中\u十六进制   html 中&#;&#后面跟的是10进制
29 == true ==1 /true  null ==0/false
30 ===全等 不会发生类型转换  !==
31三元运算符 条件运算符  条件表达式?语句1:语句2;  true执行1,否则执行2 
会执行语句并且返回结果,  c=a>b?a:b;  小心括号,运算符的优先级
32运算符的优先级  &&>||
33{}代码块,要么都执行,要么都不执行
34流程控制语句.条件判断,条件分支,循环语句
35与python不同  if只能控制他后面的一条语句,并不是根据位置分类
36 prompt() 与python的input一样 +prompt
37 switch()全等比较,必须要有break;否则一旦判断正确,后面代码全部执行  default    
 1.取余,取商,必须全等parseInt(num/10) case 6:case7连写
 2.switch(true) case code_1>code_2   相等,开关的时候才用switch
38 while(){} do while() 
39 for(var i=0; i<10;i++>){}  初始化,条件,更新表达式  
40为循环语句创建标签 label:循环语句   break label:打断指定循环loop continue 跳出当次循环 也能跳至标签标签
41 console.time();  console.timeEnd(); 字符串名字作为参数
42Math.sqrt();  对某个值开方
43object  复合数据类型  
 1.内建对象  自带的方法库  2宿主对象 由js的运行环境提供的对象 3自定义对象 开发人员创建

 2. var clc = new Object();
使用new 关键字调用的函数,构造函数constructor  构造函数是专门用来创建对象的函数 增删改查 delete clc.name
44.有符号整数,32位为符号位,0为正数,1为负数
45负数是用二进制的补码存储的  补码即为绝对值,取反➕1
46按位非 ~  Num =25 ~num=-26 num1=26 -num-1=26  
    按位与  两1为1,有0为0  and
    按位或  | 有1为1,两0为0
    按位异或 ^相同为0,不同为1
    有符号,无符号<< 左移动  左移不会影响符号位,-2 左移为-64,空缺补0 
    >> 右移 有符号右移  左边空出,补的是符号位的值 对于正数来说,结果相同
    >>> 无符号右移    空缺位补0
47 逻辑与,逻辑或返回值不确定,逻辑非返回boolean
48 for in 迭代语句,枚举所有的属性
49 with 将代码块的作用域设置到一个特定的对象
50 property  对象的属性名可随意,不推荐
 就是字典 clc["property"]=value  clc.property=value 两种访问方式   
51 in 运算符  property in object
52 堆栈  栈  堆   基本数据类型在栈,引用数据类型在堆
创建变量开辟栈,创建对象开辟堆,   引用数据类型在栈里存的值是堆的地址 
53 比较object == 比较的是在栈中的地址
54 直接创建 var clc =new Object();  var clc={}; 创建要分号
55 函数(这种方法为构造函数)  var clc = new Function("填的是字符串"););  函数具有对象的功能,能够存储数据 少用
56 函数声明 function clc(){};   var clc=funtion(){}  匿名函数前要加var clc不然报错 或者加括号(function(){})
57多余少余的实参会ignore 不会error 
58return 空;或者没写,默认返回undefined
59 函数作为参数传递给另外一个函数  fun_1(fun_2,2)不用写括号  fun_2();调用函数,传递函数返回值   fun_2函数对象
60当return为函数对象时,比如在fun_1中返回fun_2,fun_1()();就等于调用fun_2;
61立即执行函数 或者加括号(function(){})();
62var Document={  "write":funtion(){}}
63 创建的对象都会作为window对象的属性保存
64var 变量声明在所有代码之前  无var 不提前
65functionclc();函数的声明,创建提前.这就是()function clc{}  和 ()varclc=function(){}的区别 
 声明和赋值的却别,,在最上方声明 ,变量和函数,在   赋值
66函数可以改变全局的值 函数中不写var就变成全局变量
67 函数的形参,如果没有传递,不会报错,等于在函数域中创建了一个值为undefined的变量
68解析器在调用函数时都会像函数内部传递进一个隐含的参数 this 调用函数,this指向window,调用方法,this指向调用对象,this 函数执行的上下文对象
69 希望对象自己中的子函数对象能够访问到父对象的属性,使用this.属性
70 工厂函数构造对象,对比类,多了一个创建对象,返回对象的过程
71 创建出一个构造函数  
function person(){}  var clc=new Person(); Person();typeof clc为undefined  new Person();typeof为object
72 var clc = new Peron();new关键字会在person函数中创建一个对象,返回一个对象
73构造函数的执行流程1.立即创建一个对象2.将新建的对象设置为函数中的this3.逐行执行函数中的代码4返回一个对象
74 对象 instanceof 构造函数,yes return true   检测任何东西在对象中吗
75class P{constructor(){}}  一样了   
76 clc["property"](value); 调用clc对象中键为property对应的函数,带入参数value
77 提升空间,将对象中的函数提取到全局中
78 原型对象prototype 创建的每一个函数,都会往期中添加属性,prototype属性对一个对象地址
79构造函数的一个属性.prototype和他构造的对象的属性__proto__指向同一个对象一堆儿子和老爹指向一个地址
同一个类的所有实例都可以访问这个原型对象
80 Person_infomation.prototype.name==(clc.__proto__.name)/(clc.name) 先在自身找,再去原型对象中招,再去原型对象的原型对象找,最后是object对象,object no proto对象
81用in检查属性是否在对象时,如果属性在原型中也会返回in, 使用clc.hasOwnProperty("name"); 本身在原型对象的原型对象中  clc.__proto__.__proto__.hasOwnProperty("hasOwnProperty");
82在函数体中可以通过arguments对象来访问这个参数数组,参数在内部是以类数组形式传入
83arguments对象只是与数组类似,并不是array的实例,可用方括号访问,length确定参数数量,
84用arguments[0]访问,设置不用设置形参实参 typeof 为object,可以利用这点实现传入个数不同得参数
85重载函数,函数名相同,参数表不同
86ECMAscript函数没有签名,因为其参数是由包含零或多个数组来表示的,没有函数签名,做不到真正意义的重载
87ecmascript 中 return ; is establish default is undefined ,
88javascript变量松散类型的本质,决定了他只是在特定时间用于保存特定值的一个名字而已.无须决定变量类型
89所有的函数传递参数都是传递值,把外部的值复制给内部的值
90访问变量有两种方式,按值访问,按引用方式访问
91所有的环境都有一个与之关联的变量对象,环境中的所有变量,函数都在这个对象中,window?
92ecmascript 没有块级作用域,if for 创建的域为全局
93数组对象array  var clc= new Array();
94可以直接修改lenth的长度,变长,会创建出empty items,变短会删除items
95arr[arr.lenth]= 往数组的最后添加 Array(1,2,3,),[1,2,3,]两种初始化method,区别array中只有一个时,值为长度
96push()往数组后添加,随机个数的元素,并返回新长度 pop()相同  unshift()添加前面 shift();转移前面的
97 for in 对象 打键,数组打索引  for(var i=0;i<arr.lenth;i++)
98forEach();方法需要一个函数作为签名,forEach(function(){});像这种由我们创建不由我们调用的,成为回调函数
    array.forEach();数组有几个element,就调用几次函数,每次调用时,会传递三个参数
 99a.forEach(function(value,index,obj){console.log(arguments[0])}) 为什么是0,每次只传一个,每次传的不同
 100slice 切片(start,stop);可以为负数, 将数组切片,不改变原数组,
 splice 会删除原数组,并将删除值返回(1,1,"")第一个为开始的索引,第二个parameter为删除的数量,插入位置为索引位置的前面
 101arr=arr_1.concat(arr_2,arr_3,element)连接多个数组和元素 
 102 join();将数组中的所有元素转换成一串字符串,通过指点符号间隔,default 为,
 103reverse();翻转数组,sort();会影响原数组,按照unicode排序
 104. a.sort(function(){return arguments[0]-arguments[1];});自定义,return小于0换位置,其余不换

 106 this 上下文对象,argument封装实参的对象,类数组的对象.argument.lenth实参的个数 argument.callee放回指向函数的对象
 107 var dat=new Date();  getdate();获取日 getDay()周几 0为日 getMonth();月 0位一月 Date.now();当前时间戳
 108 方括号访问法的优点就是可以为变量,字符可以有特殊字符,可以为关键保留字,.访问不行
 109instanceof 操作符,判断对象是不是array对象,问题在与框架不同时,会属于不同得构造函数,
 可以用Arry.isArray();完美解决
 110栈是一种LIFO last-in-first-out 后进先出,项的插入叫推入,移除为弹出
 111 Mathn.abs();返回绝对值 math.ceil向上取整 floor向下  round   random 0到1的随机数
  console.log(math.round(math.random*(y-x)+x))  生成x-用的数     max(); min)(); pow(x,y)x的y次幂
112包装类,构造处基本数据类型的对象, new +Boolean();Number();String(); 括号内填value
113 方法和属性只能添加给对象,基本数据类型为什么可以访问方法呢,因为环境会临时使用包装类将其转换为对象.
114indexof(),lastindexof(),] 两个参数,要找的项还有找的位置开始索引 可检查string或者array,无返回-1
115 字符串在底层是以字符数组的形式保存的   charAt()和根据索引获取字符相同 charCodeAt()
116String.fromCharCode();可根据unicode获取字符     toUpperCase();
117正则表达式  定义一些字符串的规则  
创建正则表达式的对象 var reg = new RegExp("正则表达式","匹配模式")  regular expression
匹配模式 "i" ignore 忽略大小写    "g"global   "m" multiline 多行模式,查找下一行
reg.test(str);检查str满不满足reg  regular  返回boolean  检测str是否含有reg定义的正则表达式 
var reg=/正则表达式/匹配模式;  |表示或者 /a|b/  []中括号里也为或的关系/[a-z]/a到z的字母 
[A-z] 所有字母  [0-9] 任意数字    /a[bce]c/ abc,acc,ace..  [^ ]除了  有其他,比如除了ab,abc也是true
118 split 字符串拆分,可传递一个正则表达式,原先只能根据传入的死值拆分,拆分为数组  g默认全局
119 search () 搜索字符串的指定内容,返回第一个索引,对比indexof 可以传正则,可以搜索多个值,g无效
120 match(/[A-z]/gi);从一个字符串将符合规则的提取出来,返回为数组,default,默认提取一个,g,全部提取出来
121 replace("","")替换,接受正则  g全部替换
122 var reg= /a{3}/ 量词,出现三次 /ab{3}/abbb /(ab){3}/  ababab  , b{1,3}  b  bb bbb 一到三次 {m,} m次以上 
123 n+  至少一个,相当于 {1,}   n*  {0,}0个或多个  n?  相当于{0,1}0个或1个  [^a] 有没有除了a以外的字符
124 /^a/  整个字符串是以开头为a   /a$/ 啊结尾
125 元字符 . 匹配字符,除了换行和结束符  new regexp("\\两个斜杆转义")  字面量一个
\w 查找字符字母数字下划线  \W除了小w  \d数字   \D除了数字 \s  空格   \S 除了空格 \b单词边界  \B除了单词边界
\b作为单词边界和纯空格不一样,单词边界是空格或者无比如在最后面的时候   [A-z0-9]任意字母数字
126 dom document 文档 html  对象 element content 模型model  体现节点与节点的关系
127 Node 节点 网页的基本组成部分 eg:元素,属性,文本,注释,整个文档 
nodename nodetype nodevalue 
文档节点 #document 9 null   元素节点  元素名 1 null  属性节点 属性名 2 属性值 文本节点 #text  3 文本内容
128document 浏览器为我们提供的文档节点对象,对象是window的属性,
129 event 用户交互瞬间  获取元素为对象,获取元素名,类名,返回的是一个类数组对象
130 script 属性  defer先下载后执行, async下载的同时渲染页面
131 window.onload=function(){};  btn.onclick=funtion(){}
 document.write 会覆盖整个页面 w3school的官方说明：您只能在 HTML 输出中使用 document.write。如果您在文档加载后使用该方法，会覆盖整个文档。
 132 getbyid(); getbytagname();getbyname();name属性,表单项  
 元素节点 可直接通过点访问属性,读取属性  除了class  为保留字 要用  .className
 133 获取元素节点的子节点    
 property childNodes所有子节点,firstchild第一个子节点 lastchild最后一个子节点  空白节点也是节点
children  子元素 firstElementchild第一个子元素,兼容性差点  lastElementChild
134 获取父节点和兄弟节点 parentNode 当前节点的父节点  previousSibling前兄弟  nextSibling  后兄弟
parentElement     previousElementSibling  nextElementSibling
发现重复性代码就想办法创建构造函数
135  innerHTML获取文本内容 包括标签,innerText 获取文本内容,ignore tag  
136 文本节点的文本内容就是 文本节点.nodeValue   
两个思路,找到元素节点,innerHtml,text文本内容直接找到文本节点.nodeValue bj.innerHtml=bj.firstchild.nodeValue
137 function caller 该属性为一个指针,指向拥有arguments对象的函数,
138function.lenth 为形参的个数,希望接受参数的个数,定义参数的个数
139 为什么想不到,直接取反 items[index].checked=!items[index].checked;
140先实现功能,再优化
141var body=document.getelementbytagname("body");=  var body=document.body;
142 var html=document.documentelement    document.all =getelementbytagname("*"); 页面的所有元素
143 document.queryselector("css的选择器"); 支持ie8 , 可以为.class #id  但只会找到一个
document.queryselectorALL() ,可以找到多个
144 dom增删改查 document createlement("tag name");   createTextNode("text") partentnode
appendchild(); 往父节点添加子节点   插入 父节点.insertBefore(两个儿子,)  替换replacechild()
removechild();   innerHtml +="<li>XX</li>";
145 创建li,文本node,插入插入,获取ul,ul整个innerhtml+=,结合法创建li,li.inner,插入
146 取消anoclick默认行为,return false 或者 a跳转地址为 <a href="javascript:;"></a>
147 confirm();确认取消框 返回boolean值
149 dom修改css  node.style.属性=值"" 但含有-号的JS中非法,去掉-,后面的单词驼峰  
150 obj.currentStyle.width ,ie独有的   没设置通常返回auto
其余用 getComputedStyle(div,null) 样式的元素,伪元素通常为null返回对象 读取的是当前的层叠的样式 返回具体值
这两种方法都是只读的 window.getComputedStyle(div,null)  区别在于,找不到变量,error,找不到属性,undefined
function getStyle(obj,property){if(window.getComputedStyle(div,null)){return getComputedStyle(obj,null)[property]else{ return obj.currentStyle[poperty]} }return window.getComputedStyle?表达式一表达式二}
151 clientHeight ,clientWidth返回的是填充 获取可以计算的value只读可见的高度,会随着隐藏,视口变化,会减去滚动条
152 offsetWidth  offsetHeight   边框盒    
153 obj.offsetParent   获取元素定位父元素   obj.offsetleft 垂直偏移量 offsettop 水平偏移量
154 scrollWidth  scrollHeight 滚动的实际宽高 scroolleft 滚动条距离左边的高度 scrolltop 滚动条距离上边的距离
155 scrollHeight-scrollTop==clientHeight 垂直到底 scrollwid-scrollleft=clientwi 水平到底 chroemhtml iebody
156 滚动高度 如果父元素被子元素撑开,父元素的滚动高度等于子元素的    scrolltopscrollleft 不断增加
157 onscroll 监听滚动  onmousemove 监听移动  事件对象 event触发时都会传递一个event parameter
158 ie8一下,event作为window.event传入  
报错为undefined if(!event){event=window.event}   event=event||window.event;
159 clientX;  clientY;的坐标总是相对于视口的  pageX pageY相对于整个页面 事件绑定诶document.整个页面
160 var scx=document.body.scrollLeft||document.documentElement.scrollLeft; 使client  offset
161 event bubble 向上冒泡,触发子元素也会触发父元素的相同事件,向下冒泡,事件bind,向下copy event
event=event||window.event取消冒泡 event.cancelBubble=true;
162event 事件的委派,统一绑定给元素的祖先元素,利用的是冒泡排序
event.target 访问的是触发事件的对象 ul>li  target即为触发的li
164Event 对象代表事件的状态，比如事件在其中发生的元素、键盘按键的状态、鼠标的位置、鼠标按钮的状态。
事件通常与函数结合使用，函数不会在事件发生前被执行！
165 事件绑定btn.addEventListener("click",clc,false)1不要on2回调3是否在捕获阶段触发事件,通常为false顺序FIFO
    ie8 btn.attachEvent("onclick",clc)  赋值用|| 函数用三目运算 或者定义函数获取返回值,执行顺序LIFO
166  .addEventListener this 为调用的obj  attachevent 为window
167  call();apply();让函数成为任意对象的方法,使用方法同时也会调用函数 fun.call/apply(obj);可以将一个对象传递进去,函数中的this指向obj  其余的parameter,call();对象后面跟,apply对象后面跟一个数组,所有的数组装参数,
168 回调函数,当触发什么事件时,或执行函数中的函数时,回调函数不能使用函数方法 call(obj); 在回调函数中再次主动调用函数,即可用这个方法 clc.call(btn);
169 微软认为从内向外传播,网景认为从外向内创播事件的传播  
1.事件的捕获 从外往内捕获 2.目标阶段3冒泡阶段,从内向外传递  改变add的false就改变了触发顺序  
170 onmousedown  addEventListener onmousemove onmouseup removeEventListener
171 onmouseup return false; 执行这个事件时,阻止执行默认事件,当用方法绑定函数时,调用event.preeventDefalut();
172 处理ie  捕获事件  bOx1.setCapture();box1捕获所有的相关事件 取消不掉默认行为,就强行绑定
173 div.onmousewheel=function(){ 滚轮响应  火狐的函数为DOMMouseScroll,且只能用addevent来操作
 event.wheelDelta   向上为正,下为负  火狐为 detail 向上为负
 fun&&fun();有这个函数就执行
 174 onkeydown  onkeyup  按键不送开始,不断触发onkeydown,第一次和第二次有一点间隔 只能绑定给input或document
 175 event.keyCode 触发事件的unicode  altkey shiftkey ctrlkey同时被按下
 176 在表单元素中输入内容时默认行为,return false 就死了
177 bom browser object model 操控浏览器  Window Navigator Location History Screen 都是作为window的属性save
Window 代表整个浏览器窗口 全局对象 Navigator 当前浏览器的信息,识别不同得浏览器
Location 当前浏览器的地址栏  Screen 用户显示器的相关信息
 History 浏览器的历史纪记录 因为隐私问题,不能获得具体历史记录,只能操控向前向后翻页,该操作当次有效
 178navigator.appName 以前用于分辨ie和其他,现在逐渐失效  useragent===浏览器browser
 179 /chrome/ig.test(chrome)  firefox  ie 为msie  ie11 edge为
 178 ifwindow.ActiveXobject 但做了手脚 有为ie "ActiveXobject" in window in操作符传的是字符串,这个对象有没有这个属性
 179 history .length 访问到当次访问页面总数量  history.back();和后退一样 forward();前进
 go();正数作为parameter 跳1个,往后跳-1
 180 location 可以修改为一个路径,并且会生成对应的历史记录
 location=" " ==location.assign("") location.reload(true):刷新页面  传true 清除cookies
 location.relace("href") 区别在于不会生成历史记录,不能退回
 181 定时器 setinterval(fun,ms);window的属 返回值为定时器的标识,clearinterval();接受null,undefined不会error
 index =index %img.Arr.length 
 182 全局定义, 局部赋值   1,开启之前关闭上一个,2判断开启
 183 如果在onkeydown 创建定时,不松手会不断的创建定时函数
 184 延时调用settimeout(2000)
 185if((speed>0&&modify_value>target_value)||(speed<0&&modify_value<target_value))
 想破脑袋都要想出合并方法
 186 把定时器标识添加到对象自己的属性中,防止别人误触
 187 我是构造了一个按键函数,speed只传入了一次就没了,老师是在按键后带入函数,每次按键都重新传参数
 188 callback 在动画完毕以后再执行一个动画,完毕很关键,执行完毕之后
189 因为是先创建响应函数,把i储存到对应数组元素的一个属性中,在oc fun中用this访问
190 样式等于一个空串,就可以让原先的样式优先
191 搞清楚函数的发生顺序,放在回调函数可以保证先前的函数运行完毕,如果独立分开,会导致运行过程中,下一个函数运行对结果产生误差
192 retain original syle obj.className+=" claaName" 记得空格
193 ul.style.height=""; 把内联样式表重置 
194 制造出越多的相同,越能合并成一个相同的函数 
195 JSON 特殊格式的字符串,可以被任意的语言识别,并转换为任意语言的对象
JSON JAVASCRIPT OBJECT NOTATION JS对象表示法  json 中的属性名必须加双引号 字符串 数值 布尔值 null 对象 数组
obj='["name":"chenlicheng","gender":18]'   arr='[1,2,3,true,"hello"]'
196 js 中有一个对象叫做JSON JSON.parse(json字符串) 将JSON为js对象  jsonie7 can;t useless
JSON.stringify();将js转换为JSON
197 eval("alert(123)"); 可以执行一段字符串形式的js代码
eval("("+clc+")"); 如果clc为一个含大括号的,会当成代码块,需要加上括号,执行性能比较差,还有安全隐患,比如用户如果传的是代码块,就会执行  ,兼容ie7 引入一个json文件
198 window.$ 向全局暴露一个函数,即使是在IIFE中,return(test:test)
199 不写分号,除了[] () / + - 会发生解析错误,return ,break、continue、throw,如果换行会自动添加分号,可在前加
200 函数都有一个属性,prototype指向函数的原型对象,对象都有一个属性constructor 指向函数
201 实例对象不需要通过用__proto__去访问原型对象中的属性,他自己回去找,但是设置自动就在其属性中设置
  clc.a  在__proto__中,clc.a=3,在clc中
202 全局执行上下文 1 var 定义的全局变量添加为window的属性, 2函数变成window的方法 3 this,指向window
函数执行上下文 1实参赋值给形参,为函数执行上下文的属性,2argument为实参类列表,3var 局部变量为属性,
4fun为函数的方法,this 为调用函数的对象
203 闭包当嵌套的子函数用了父函数的变量 执行外部函数,不用执行内部函数,就产生了闭包,闭包是存在嵌套的内部函数中
调用一次外部函数,就产生一个闭包,闭包内的引用外部的数据不会被释放
闭包可以理解成“定义在一个函数内部的函数“可以访问外部函数的变量,
1.let 块级作用域, 2闭包 (function(i){})(i)  3. 保存在对象的属性中

scrollIntoView  动画滚动效果

空数组布尔值为 1 字符0布尔值为1

map,filter,foreach 可直接传一个参数,参数为函数名,会把数组每一个元素传入这个函数