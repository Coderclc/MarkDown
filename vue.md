
132 git
版本控制,版本迭代,主流的版本控制器有 git SVN,cvs,vss,tfs
本地版本控制 集中版本控制 SVN(版本保存在同一个 server)协同开发同步更新 分布式版本控制(所有版本信息都同步在本地的用户中)
git 是目前世界上最先进的分布式 ban'b 控制系统 ,是 linux 创始人用来替代 bitkeeper 的
Git bush unix 与 linux 风格的命令行 ,使用最多 recommend 最多
git cmd windows 风格命令行
git gui 图形界面 git
basic linux command   
1.cd 进入 2 cd.. 上一级 3 pwd 显示当前路径 4ls(ll)列出目录 ll 更详细 5 touch touch index.js
新建文件 6 rm rm index.js 删除文件 7mkdir 新建文件夹 8 rm -r 删除文件夹
9 mv mv index.js src src 目标文件夹 10reset 初始化终端 11clear 清屏 12history 查看命令历史
13 help 帮助 14 exit 退出 15#表示注释 16 rm -rf / 删除 linux 所有文件
git config -l 查看 git 所有的 list 配置清单
git config --system -l 查看系统本身的配置清单
git config --global -l 查看用户的配置清单
D:\Program Files\Git\etc\gitconfig 系统的配置文 user 下的 git config
$ git config --global user.name "Chenlicheng"  配置了才可以上传
$ git config --global user.email "804748585@qq.com"--global 为全局配置,若想要项目使用不同去掉-g
搭建本地仓库 git init 克隆远程仓库 git clone [url]
git add . git commit -m " 注释"
.gitignore   syntax
1.#为注释 忽略 ,2 linux 通配符 * 号表示任意个字符,?问号表示一个字符,[abc]方括号为可选范围
{string1,string2} 大括号为可选字符串
*.txt 忽略所有.txt 结尾的文件  !lib.txt 除外 
git add filename  git reset filename  ==git rm --cached filename  workdir 和stage切换
查看状态  git status  git status -s   查看更改  尚未缓存的改动：git diff   
git commit -am '修改 hello.php 文件'   跳过modify再次提交stage
git rm <file>   git rm -f<file>  跟踪过 强制删除,  git rm --cached <file>不删除文件,删除track
git branch name  创建分支   git checkout name  切换分支  git branch -d name 删除
git log  查看提交历史  git fetch  gei merge ==git pull
git remote add origin git@github.com:tianqixin/runoob-git-test.git
git push -u origin master
git pull supermall  master
git reset -hard 放弃本地所有修改
git clean -df 移除一些创建的文件夹
linux  vim 文件名 :w   保存文件但不退出vi :w file 将修改另外保存到file中，不退出vi:w!   强制保存，不推出vi:wq  保存文件并退出vi:wq! 强制保存文件，并退出vi:q  不保存文件，退出vi:q! 不保存文件，强制退出vi:e! 放弃所有修改，从上次保存文件开始再编辑
列出已有的tag  git tag
新建 tag  git tag v1.0
git tag -a tagName -m "my tag"  -a是指令  注释写在后面
git show  查看git  tag
删除  git tag -d v0.1.2    打了tag以后也要提交到服务器git push --tags
git log  查看当前有哪些commit
git push origin b589ff688:master 提交指定commit
git reset --hard  加哈希值   在log可以看到哈希,复制部分即可
git checkout  切换分支

135 vue cli3 config 3中方法 1. vue ui    2隐藏在@vue中 cli_service
3.只能起名 vue.config.js 通过module.exports={} 用户自定义级别会高于default
136 arrow function  const clc = () =>{}    parameter list 
函数只有一行时 const clc = x => x  自动把x返回 匿名函数作为参数调用时最多
137 箭头函数中的this引用的是最近作用域的this,箭头函数无this定义,往外找
138 vue router 路由是数据包从来源到目的地的路径 转送是将输入端数据转移到合适的输出端
139 后端渲染,通过jsp技术java serve page 在后端将页面渲染好,在放到前端  
后端路由 后端处理URL和页面之间的映射关系
140 前端渲染,先从静态资源服务器,把html+css+js拿到前端渲染,再从api接口服务器请求数据
后端提供api来返回数据,前端通过ajax请求数据
SPA 单页面富应用 simple page web application
前端路由 映射 url /和大的组件切换映射关系
141 window.location.href=""  通过hash改变location ,页面不会刷新
history.pushState({},"","/home")  history.back() 类似栈结构
history.replaceState({},"","")  不能返回
history.go(-2)弹栈, 正数 压栈 history.forward()=history.go(1) history.back ()=history.go(-1) 
142 导入路由插件,调用vue.use()安装plugin,创建路由实例,传入路由配置,在vue实例中挂载路由实例
vuerouter options 为 routes  vue option 为router
144 mode:"history" 切换为dom history 后缀模式 ,
143 router-link router 内部注册的组件 <router-link to="./home">首页</router-link><router-view/>
默认渲染为a标签  tag="button"  布尔属性 replace  不能返回
被选中的router-link 会自动添加类名 router-link-active,,可以通过属性active-class="active"修改生成的类名 也可以通过创建router instance option linkActiveClass:"active "
144 不同router-link 采用原生 history.pushState({},"","home")false  用不了  this.$router.push("home")this.$router.replace("home") 重复跳转相同时回报错,尚未解决
145 添加routes 时 ,path :id_name对应的可以为任意值
$route.params.(id) 活跃状态的 routes选项 route 的参数 id,id为setvalue
146 打包好的文件,app开头为user写的代码 ,vendor 为第三方,vue,vue-router/axios,mainifest底层支撑
意思就是es6的语法,export都是由一些底层特殊的函数方法解析的,这些函数打包到mainifest
__webpack__require__ 把所有模块放到一个数组作为这个函数的参数
147 lazy 把路由对应不同得组件分隔成不同得js文件,访问时才加载   .map 变量替换元数据
component:()=>import("path")   需要渲染时才去服务器请求 懒加载
148 1. 结合vue的异步组件和webpack的lazy load
const Home =resolve =>{require.ensure(["./componnetns/Home.vue"],()=>{resolve(require("./components/home.vue"))})}
amd 2.const About =resolve=>require(["./components/About.vue"],resolve)   AMD写法
149 routes option 与path同级  children 子routes  detail  childroutes path"" 不加/ ,to=""都要加/
150参数传递 1 . $route.params.(id) 点击 user s时,把users.vue的数据传递到url,在通过$ro.pa fetch
需要载体 :id
id  /path/:id   :to="/path/+id"  动态获取id  this.$router.push("/details/"+this.item.iid);
query  /path    :to="{path:'',query:{name:''}}" this.$router.push({path:'/details',query:{}});
URL统一资源定位符 协议 主机名端口号路径?查询query&间隔 #片段 哈希值
scheme://host:port/path?query(&query)#fragment
151 将vue option 中的 router 放到vue.prorotype中 在源码中
152 组件对象的__proto__指向的是一个vue 的实例,所以Vue类对象的prototype指向的原型对象 ==组件对象的__proto__.__proto__
所有的组件都继承着vue的原型x
153 组件的生命周期函数 options,created(){} 组件被渲染出来是运行,mounted ,模板,挂载完运行
updataed(),页面发生刷新时运行
154监听路由改变,可以路由的全局导航守卫,原生方法 
router.beforeEach((to,from,next) =>{ document.tiitle=to.title
  next()}) 前置守卫 guard
 to 是一个route类型  给选项routes路径下添加配置 meta:{} 元数据
通过to.meta.title  或者to.matched[0].meta.title 获取 因为第一个路径有一个两层的默认路径
afterEach((to,from)=>{})  后置钩子 hook每一次路由切换时 不需要next 这两个每次切换都运行
beforeEnter: (to, from, next)路由内守卫,只有切换这个路由运行,还有三个组件内守卫
beforeRouteEnter  beforeRouteUpdate (2.2 新增)  beforeRouteLeave 监控组件内的守卫 进入离开更新
155 每一次切换router,都会重新渲染router-view 组件,keep-alive 组件避免重新渲染
156 vue生命周期函数 crated(),destroyed(),activated();deactivated();这两个函数不是生命周期函数,
 $router.push 会把所有的路径都替换了  只有被keep-alive包含act,de函数才有效,函数是写在组件内的
 157 keep-alive 只有router-view被keep-alive包围时才有效.有两个属性,include,exclude,填正则表达式,匹配的才缓存,匹配的不 缓存  组件内的name:"" include="name,name1"
 158 在script 标签中引入 用import  "" import("") 在style 中用@import
 159tab-bat-item 的高度大部分是49px
 160 思路现在 app.vue 实现全部功能,再逐渐抽离分装
 161 register 的时候 tabbarItem  使用的时候可用短横  <tabbar-item><tabbar-item>
 162 给slot 加一层div 的包装,防止插槽替换的时候覆盖掉
 163 传字符串不用:数值要加: :cmessage="message"path=/home""
 164 我一开始的思路是想着点击那个哪个就变红,其他不红,老师的思路是让他自己计算,自己判断该不该变红
 165 a.indexOf(b)  如果  在a没有找到b,就返回 -1
 166 起别名 '@': resolve('src'), 'assets': resolve('src/assets'), 
 在html中attr使用要加~  css backgroud:url(~@/assets/img)





<script src="./js/template-web.js"></script><div id="app"></div>  <script id="tp1"type="text/html"><div class="box">{{username}}{{age}}</div></script>  <script>const html=template("tp1",{username:"chenlicheng",age:18})document.getElementById("app").innerHTML+=html</script>
<script>   {{each info}}{/each} 循环 template.defaults.imports.dateForMat=dateForMat 向模板暴露一个函数,跟vue 的computed 一样
验证邮箱,在前端验证规则 ,服务器验证是否可用
FormData 对象 模拟表单 ,将html表单映射成表单对象,自动将表单的数据拼接,异步上传二进制文件
const formidable=require("formidable")
const formdata = new  FormData(form node)Tip: 不能设置setquesthead的数据类型,
服务器设置const form=new formidable.IncomingForm()form.parse(req,(err,fields,files)=>{res.send(fields)})   advantage不用去拼接 所以必须要设置name的属性,
FormData instance attr   formdata.get("input.name")  formdata.set("input.name","value")已存在,替换,不存在,创建  formdata.delete("input.name") 删除表单对象中的属性和值 
formdata.append("key","value") 创建一个空的表单对象 const f = new FormData() 然后append或者set
append 会都保存 error默认接受后一个,可f12,setcover  
FormData upload 二进制文件jpg,video,audio
file.onchange 文件添加时触发, 切记 箭头函数中的this指向最近作用域的this
formdata.append("attrName", file.files[0]) 空formdata添加
form.uploadDir = path.join(__dirname,"public","uploads")设置上传文件的路径
默认传过来为二进制文件,无extension  form.keepExtensions=true
xhr.upload.onprogress=(ev)=>{bar.style.width=(ev.loaded/ev.total)*100+"%"bar.innerHTML=(ev.loaded/ev.total)*100+"%"}   文件上传的过程中会不断触发
页面显示img ,上传的图片都会保存到public下的uploads,截取"public字符"动态生成img,防止用户看到img加载
同源政策 ,如果两个页面具有相同的scheme,hostport即为同源
使用JSONP  jsonwithpadding 不属于ajax ,模拟ajax请求,用的是get方法
srript 标签 src引入一个外部的js文件不受同源限制的影响 所以script引入一段"fn(data)"字符串可以直接执
const fn = req.query.callback+"({name:'chenlicheng',age:18})"res.send(fn) 后端服务operate
在onclick下创建 script标签,在script.onload之后删除,在请求时把函数名通过query传递到后端
每调用一次jsonp() 相当于执行一次fn(data),data来源于后端
jsonp后端需要返回一个字符形式的"fn()",对象抽离,转换成字符串,拼接+"(",res.send("fn()")
可直接用res.jsonp(obj)完成   const obj = {name:'chenlicheng',age:18}
const str = JSON.stringify(obj)const fn = req.query.callback+"("+str+")"res.send(fn)===res.jsonp(obj)
CORS cross-origin resource sharing 跨越资源共享 非同源ajax
当不同源时,请求头会添加一个attr origin,当服务器同意时,会在响应头 add(Access-Control-allow-Origin)
浏览器根据响应头有无这个属性判断出服务器是否同意这次请求
res.header("Access-Control-Allow-Origin","*") 允许所有源向我发出请求 *也可以填请求origin
res.header("Access-Control-Allow-Methods","get,post") app.use((req,res,next)=>{next()}) 拦截所有请求,操作所有响应
cors 同源政策是浏览器给ajax技术的限制,服务器端不存在这种限制,可通过自己的服务器去访问
const request=require("request")request("http://localhost:3000/ajax",(err,response,body)=>{})
Cookie HTTP协议默认是无状态协议,cookie 实现了身份识别的技术,先响应cookie再发送cookie
跨域时不会发送cookie信息, 通过属性withCredentials default 为false 可以携带cookies
并且服务器端 Access-Control-Allow-Credentials
$.ajax({type,url,data:{namae:"chenlicheng"}/"name=chenlicheng",contentType,beforeSend:()=>{return false},success:()=>{response},error:()=>{xhr}})
无论data是传对象还是字符串都会转换成urlencoded format
beforeSend定义在xhr.send()之前,可通过return false 取消这次发送,响应成功success失败404,500error
无论是get还是post urlencoded/json 发送的都是字符串形式 如果发送是对象的字符串,服务器接收到都会.query .body转换成JS对象
$().ajax  发送 formDate  processData :false,  不要去处理数据,contentType : false,不要设置请求头  
$(). 对象的方法 const str = $("#form").serialize() 拼接表单为urlencode format
$.ajax({dataType: "jsonp",url: "/jsonp",jsonp:"cb",jsonCallback:"fn",success: (response) => {console.log(response); jsonp请求
},})  jsonp  change server follow change cb  jsonCallback:"fn" 更改函数名,需要另外定义函数
$.get/post(url,data,success(resopnse ))
disable selecttion 
document.onselectstart = new Function("event.returnValue=false"); all
dom.onselectstart =function(){return false};  part of
disable open menu 
document.oncontextmenu = new Function("event.returnValue=false"); 
Ajax的全局事件 jQuery方法,只要有Ajax发送就会触发,无须设置 beforeSend()
$(document).ajaxStart()请求开始发送时触发   $.ajaxComplete()  $(document).on("ajaxStart")
NProgress 引入 css,js 文件  NProgress.start() — shows the progress bar 
 NProgress.set(0.4) — sets a percentage  NProgress.inc() — increments by a little
NProgress.done() — completes the progress 
RESTful API :  GET 获取  POST 添加  PUT 更新  DELETE 删除  tradition unsupport back two
ajax suport  get users/1 获取id为1的用户信息,把id添加到route而不是query
ajax "users/1"  server  "users/:id"  req.params.id
ecma6语法  `${id}`
XML 语言被设计用来传输和存储数据。 eXtensible Markup Language 重点在于传输和存储数据
HTML 用于展示数据   
获取XMLDOM  XMLdom.getelemtns by("tagname") 获取节点.innerHTML获取信息







 debounce 防抖,将上一个定时器关闭  clearTimeout(timer);timer = setTimeout(() => {console.log("我只执行了一次");}, 300);
 封装 debounce(fun, delay) {let timer return (...args) => {timer && clearTimeout(timer);timer = setTimeout(() => {fun.apply(this, args);}, delay);};},
理解 const args = 一个数组,包含了所有传入return 的心函数的参数   args是一个数组
...agrs 把数组args 拆开 所有的参数放在这里 |创建了一个数组,所有的参数都放在数组内
最终的this.新生成的函数放到一个对象内,那么this就是这个对象,但是return 的函数不能写箭头函数,因为对象key:对应箭头函数时,this指向对象外的作用域


 /节流 throttle  一定时间内只能执行一次
 let timer=null   if(!timer){timer = setTimeout(function(){);timer = null;},wait)}
 ref 挂载到div 获取的是dom对象 ,ref挂载到组件获取的是组件对象  
 通过$el  this.$refs.tabSwitch.$el 获取dom对象 
 Object.keys(obj).length!==0
 v-if 绝对宣布渲染  v-show 绝对显不显示,所以if的层级很提前,在mounted之后渲染,
 多层级数据不是在一开始初始化的时候就获取到的,异步数据先显示初始数据，再显示带数据的数据，
创建组件,初始化数据,第一层的data,methods等,编译成rander函数,挂载el,渲染
用类将数据进行整合  v-for""在谁身上,谁就会被复制多少份
循环遍历的时候吧index读取出来就可以给key绑定index
const date= new Date(value*1000)format(data,"yyyy/MM-dd hh(HH):mm:ss") h12H24
读取多层数据的时候,读取一层二层找不到为null,undefined,三层会报错

继承 class Animals{run} class Person extends Animals{}
两个路由使用相同的emit方法时不会各自触发,但是使用相同的状态管理绑定给watch时,若组件没销毁则会触发
const unwatch = this.$watch("name",cb)   取消只能取消掉创建的,不能取消掉已经写好的


this.nextTick保证渲染完成,但是图片不一定加载好



