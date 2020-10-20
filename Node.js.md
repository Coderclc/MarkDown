<script>
shift + right  open cmd  
Node.js 基于chorme V8 的javascript运行环境
1.事件驱动
2.非阻塞IO模型 异步
3.轻量和高效
一、主要作为中间层,前端<>-数据库
- 减轻客户端内存,mvvm模式是把页面渲染和数据请求都放在客户端,压力大
- SEO(Search Engine Optimization 搜索引擎优化)性好,因为在服务端就渲染好了html元素字符,有利于被网页搜索到
- 可配合nginx,redis优化项目,应对高开发
二、项目构建工具
- webpack vue-cli 都是用node.js 写的
三、小型,个人的后端
es7 js装饰器
trigger  imp  imd  rqr  req  mde
module.exports
"exports is assigned the value of module.exports before the module is evaluated."
exports只是module.exports的全局引用  var module = new Module() var exports = module.exports
所以为什么不能写exports={} 因为exports=module.exports  不能重定义
exports.clc="chenlicheng"   module.exports.clc="chenlicheng"  module.exports={}
module.exports = App  类  
const a = require("./") a = {clc:"chenlicheng"}
多次引用只会生效一次

Npm 
eg:const $ = require('jquery');
require 加载机制-> 先找node_modules 下的同名文件 再根据文件内的package.json的
        "main": "dist/jquery.js" 找到js文件,如果没有main,则找文件夹内的index.js,找不到就在node的上一级找,直到磁盘根目录
npm -v  npm的版本
npm init  初始化package.json + -y 快速跳过
npm install  根据pa.json 下载依赖
npm i -D =--save-dev 开发时依赖
npm i -S == --save运行时依赖
npm list  查看当前目录所有node包
npm list -g  查看全局node包
npm update package 更新指定包
npm uninstall package 卸载指定包
npm info package 远程查看包的信息


fs--文件系统  file system

sync: const content = fs.readFileSync("./hello.txt",{flag:"r",encoding:"utf-8"})
async: fs.readFile("./hello.txt",{encoding:"utf-8"},(err,data)=>{console.log(data);})
function readFile(return new Promise resolve)
res.toString() 可以拿到结果
写入
fs.writeFile

删除文件
fs.unlink('test.txt',()=>{})

Buffer  以二进制的形式存取数据,以16进制显示
数组不能进行二进制的数据操作
数组的空间不是连续的,存取速度慢
buffer内存空间开辟出固定大小的内存空间,是连续的
const str = 'life is short use python'
let buf = Buffer.from(str)   // 将str 转换成buffer形式
console.log(buf);// <Buffoe xx x x x x x x x>
console.log(buf.toString());
实际上,预先开辟buffer空间
new Buff

const buf = Buffer.alloc(10)  // size = 1 byte  开辟十个字节空间
buf[0] = 255
console.log(buf);
console.log(buf[0]); 255
Buffer.allocUnsafe() 不需要开辟空间,直接用遗留的已存在的空间,但不安全

读取目录
const fs = require('fs');
fs.readdir("../NODE",(err,files)=>{
  if(err) return
  console.log(files);  //string[]
})
remove dir
fs.rmdir('wenbo',()=>{})

ReadLine  交互

writestream  读写流\

Node 事件
node.js是单进程单线程application program, 但是有V8引擎提供的异步执行回调接口,
所以可以处理大量的并发,性能很高
几乎所有的API都支持回调函数
事件机制都是用设计模式中管擦着模式实现
单线程类似进入一个while true 事件循环,异步事件都生成观察者,有事件发生就调用这个函数
一个进程一个浏览器,一个线程一个page

自己封装到对象中
内置
const events = require("events")
const eventEmitter = new events.EventEmitter()
.on .emit

数组索引值可以为字符串,但无法迭代iterate
CLS清屏 cmd 
delete key  删除对象key
传入可变参数,调用时,可一一对应,或者..args 全部放到这个数组里

内置模块
path
const path = require('path');
console.log(path.extname(url)); //获取拓展名

拼接  resolve
可以拼接  "../" 返回上一级
const path = require('path');
如果没有拼根目录,会把当前的目录拼上
不会处理多余的 / 

join
没有根目录不会拼接根目录 返回.  会自动处理多余的斜杆

parse
解析路劲

__dirname == reslove()
全局对象,当前根目录

__filename
还包括了输出这个的index.js文件

process.cwd() 执行node命令的文件夹目录名

os  操作系统
os.cpus()  cpu
os.totalmem() 内存
os.arch() 系统架构 x64 
os.freemem() 剩余内存


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
() 单独匹配一下小括号的内容
(.*?)  igs 忽略大小写,全局,使.可以匹配换行符
(n)因为括号内的(n)会被捕获  (?:n)表示不会被捕获 但返回结果不会单独捕获,但整体还是包括这一部分
?= 匹配,但返回不会被单独捕获,返回的整体也不包含这一部分
(?!cc3)  匹配不紧跟着cc3的
(?<=cc3)  匹配前面紧跟着cc3的,但结果不返回cc3
(?<!cc3)  之后
?<haha> 给组命名
reg.exec()  返回匹配到的结果
在[] 中 [.-] 就是匹配 . 和 -  
.*? 懒惰匹配   .*贪婪匹配
\cx	匹配由x指明的控制字符。例如， \cM 匹配一个 Control-M 或回车符。x 的值必须为 A-Z 或 a-z 之一。否则，将 c 视为一个原义的 'c' 字符。
\f	匹配一个换页符。等价于 \x0c 和 \cL。
\n	匹配一个换行符。等价于 \x0a 和 \cJ。
\r	匹配一个回车符。等价于 \x0d 和 \cM。
\s	匹配任何空白字符，包括空格、制表符、换页符等等。等价于 [ \f\n\r\t\v]。注意 Unicode 正则表达式会匹配全角空格符。
\S	匹配任何非空白字符。等价于 [^ \f\n\r\t\v]。
\t	匹配一个制表符。等价于 \x09 和 \cI。
\v	匹配一个垂直制表符。等价于 \x0b 和 \cK。
中括号内 \\ 要转义



url module

重点
forEach  和 for  of  都是遍历数组
遇到Promise  async 都会等待,
但是 for of 是执行完一个循环再执行下一个next()
forEach()是开启多个循环,并且所有循环执行完毕就结束了,即使函数里面有await promise也会结束循环,就会导致请求慢,循环结束,数据获取失败

异步调用 
 return  axios().then(resolve()) 相当于有一个 空的  resolve()
 意思就是返回一个axios时,默认返回一个执行了空resolve()

无论函数声明函数定义,箭头函数,async ,await Promise都会停止

cheerio jQuery核心功能的一个灵活简洁的实现
const cheerio = require("cheerio")
  // let $ = cheerio.load(res)
  // $(".col-6 .list-item .media a").each((index, el) => {
  //   const href = $(el).attr("href")
  //   console.log(href)
  // })

try catch 有自己的作用域错了 是const 赋予了他作用域

反爬虫
设置axios  proxy  设置代理池/

后端渲染,可以拿到完整界面,前端渲染,分析ajax,请求的数据

querySelector只返回匹配的第一个元素，如果没有匹配项，返回null。
2、querySelectorAll返回匹配的元素集合，如果没有匹配项，返回空的nodelist(节点数组)。

puppeteer
// eventMsg: object   monister  bom  console
page.on('console',function(e){
  // iterator print
  console.log(e.text());
})

// 返回dom节点对象数组 可以进行事件操作
const event = await iPage.$$(".col-6 .list-item .media a")
event[0].click()

浏览器内置,node没有
cnpm i xmlhttprequest
use var XMLHttpRequest = require("xmlhttprequest").XMLHttpRequest;

 page.keyboard. 在光标当前位置
 iPage.type('input#kw', '为什么文竣平喜欢打飞机\n') 在指定位置

for for i for of 一样 each不行

  // screenshot
  // await page.screenshot({ path: "./screenshot.png" })

  // const event = await iPage.$("input#kw")
// await event.focus()
// await iPage.keyboard.type('为什么文竣平喜欢打飞机\n')

elementHandle.getProperties()
page.setRequestInterception(value)
page.waitForSelector(selector[, options])

网络协议简述
协议是网络计算机通信的规则
IP TCP HTTP POP3 SMTP

协议栈
多层多种协议按层次顺序组合

应用层  HTTP FTP TFTP SMTP SNMP DNS
传输层  TCP   UDP   后端  向下为网络工程师 

网络层  ICMP IGMP IP
数据链路层\物理层    ARP  RARP

带着request header  将url 转换为IP地址,dns域名解析
TCP:添加一些信息,加port
到交换机.....

html hyper text markup language
http hyper text transfer protoco  最上层协议
client  客户端  <-> server  服务器
1.简单快速:  路径/方法
2灵活  允许传输任意类型的数据对象  用content-type 标记
3无连接  client 和server 不需链接 即可完成响应过程
4无状态  每一次都要完整的请求过程,有好有坏
5 支持B/S  C/S模式
browser - serve    浏览器和服务器链接
client -serve    客户端和服务器链接  

uri  uniform resource identifiers   统一资源标识符
http  通过 uri 传输数据,建立链接.
url 是特殊的uri  统一资源定位符 uniform resource locator
协议scheme  域名 host 端口port 路径 path  锚
请求头 

请求体

响应
状态行
消息报头
空行
响应正文

in 关键字 查键

图片路径,icon图片路径都会触发server.on request

文件夹
npm init 
注册   verify
login native  npm login
发布  publish



express 基于 Node.js 平台，快速、开放、极简的 Web 开发框架
express -h   查看express命令行指令

创建名为myapp的express应用,并且使用ejs模板引擎
express --view=ejs app
express app -e
original command
const express = require("express")
const axios = require("axios")
// build app instance
const app = express()
// listen port
app.listen(8080, () => {
  console.log("server start success: http://localhost:8080")
})
// set route
app.get("/", (req, res) => {
  res.send("<h1>hello express</h1>")
})

类正则表达式
route: "clc?why"   c可以有可以没有 类正则匹配模式
clc+why  c可以为多个 clccwhy
clc*why  中间可为任意字符
clc(why)?csq  一样,作为整体

正则模式
直接传正则表达式,不用加引号

动态路由
"/clc/:why"  why 作为一个变量接受url上的params
console.log(req.params); 可通过req查看,接受

路线处理程序
app.get("/clc", function(req, res, next){
  console.log(123);
  next()
},function(){
  console.log(456);
})
get请求
req.query
POST请求
query在req.body
const bodyParser =require("body-parser") app.use(bodyParser.urlencoded())
就可以通过res.body访问请求体内的内容

添加中间件
app.use(function(req,res,next){})  拦截操作

const route1 = express.Router()
route1.get('/',(req,res)=>{
  console.log("首页");
})
route1.get('/list',(req,res)=>{
  console.log("list");
})
app.use('/clc',route1)
把路由1的首页设置成clc
route1.use(func...) 路由的中间件

首页路径默认为/
没有也会添加,有则无视
通信应用程序都会占用一个端口号
socket.remoteAddress
socket.remotePort
Port范围 0~65536之间

text/html 会当成html渲染
text/plain

res.end(data) 可发送fs 读取的buffer res.end 可发送字符串,buffer  编码为utf-8 类型为自动

art-template
in browser
  <script src="./node_modules/art-template/lib/template-web.js"></script>
  <script type="text/template" id="tp1">
    <h1> hello <%= name %></h1>
  </script>
  <script>
    const c = template("tp1",{
      name:"clc"
    })
    console.log(c);
  </script>
<script>
后端渲染有利于seo搜索,比如商品后端渲染,comment前端
当访问浏览器时,会发送一次请求获得html,渲染html时加载图片,也是通过发送请求,
所以要处理这些图片请求,获取url  send data
res.statusCode =302
res.setHeader('Location','/')
res.end()

// 开放静态文件夹
app.use('/',express.static("./public")) 
// app.use(express.static(path.join(__dirname,"public")))
把根路径替换成 public 默认的index.html
http:可以访问,但是没有配置就不会有结果
express:设置静态文件后可自动处理结果 内部处理

res.end() http 还要设置contenttype  
res.send() express 内部封装api auto set contenttype 
nodemon  自动检测重启server

使用
express art-template混合
npm i art-template 
npm i express-art-template
html  要改成art结尾 ,并且要放在views文件目录下 views要放在根
app.engine("html", require("express-art-template"))
res.render('index.art') 通过render发送这个文件

post请求 

1.把app.  抽离到route ,但是改变了入口
2.route module.exports function  但是自定义了函数
3

packgae-lock.json 保存所有包的依赖信息
lock 锁定版本, ^ ~向上的版本

MongoDB  nosql  非关系型
关系型数据库和非关系型数据库
表就是关系,关系型数据库
 关系型数据库都需要通过sql 来操作
 关系型数据库还需要设计表结构
 数据表还要进行约束
 唯一的
 主键
 默认值
 非空

 非关系型数据库  没有表的概念
 就是key-value mongoDB是很像关系型的非关系型数据库
 启动 mongodb  mongod
 第一次执行要在安装盘符新建/data/db
 mongod  
 mongo   exit
 show dbs
 use database  链接数据库 默认为test
 db查看当前数据库
 use students 
 db 当前选中的database
db.students.insertOne({"name":"chenlicheng"})
db.dropDatabase() 删除数据库
show collections 展示集合
db.student.find() 查询集合所有的数据
灵活,数据没有限制

使用第三方mongoose

koa
app.use 挂载的函数,必须调用next才能链式调用不然只执行第一个函数
不包括挂载模块
安装body模块必须在route之前
body-parser只能解析x-www-form-unlencoded
解析form-data 必须要用koa- body模块  通过 ctx.request.body 拿到
koa-body 必须配置multipart 为true default  is false 
VARCHAR(255) 255个字节,可以放255个单词,一半的汉字,汉字是双字节
表明默认要带s,找的时候回找带s的表名字
router.post('/adduser', async (ctx, next) => {
  await userController.addUser(ctx)
});

router.post('/adduser', userController.addUser);

路由内操作要加await 不然 相应为空

app->router->controller->service->model

如果错误被 try-catch  捕获就不会触发app.on('error',fu)时间
必须手动施法 ctx.app.emit('error', err, ctx);

includes 连表操作

{

​    association: DeviceOrder.belongsTo(CommonUser, {

关联表的字段

​     foreignKey: 'user_id',

​     targetKey: 'user_id'

目标的字段

​    }

当一个函数加了async 关键字就变成了异步函数,js单线程运行到这个函数时如果这个函数是不会等待的而是开启异步.	



netstat -ano

set PORT=8081
npm start

linux:PORT=8081 npm start

