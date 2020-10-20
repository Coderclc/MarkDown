25let 块级作用域, 2 闭包 (function(i){})(i) 3. 保存在对象的属性中
26 闭包可以理解成“定义在一个函数内部的函数“可以访问外部函数的变量, 创建出来的闭包里面的引用的值会延迟消亡


 46 item.price|过滤器  option  filters:{guolvqi(a){return a }}  item.price|guolvqi  (item.price)可不写

  extend 继承 class Person{}   class student extends Person{} 
  61 1创建 调用Vue.extend()创建组件构造器 ,2 注册调用Vue.component()注册组件 3使用 在Vue实例范围内使用
  62   const component_constructor = Vue.extend({template:`code_snippet`}) Vue.component("elname",construc)
  Vue构建要放在组件构造后面


  67register component 语法糖,直接在注册时创建组件,全局局部同理
  68template 的抽离  <script type="text/x-template" id="cpn1"></script> <template></template>

  抽离,1.template抽成外部 2 Vue.extend({})括号的对象抽出来放到构造器上3对象的增强字面量写法
  在html,短横,大写,都必须用短横,小写可直接用 myCpn  -> my-cpm/my-Cpn
  在vue,短横必须用短横,大写可用大写,短横


props:[]为一个数组时,元素虽然为变量,但也要加引号, v-bind:cmovies="movies write in cpn instance
props:{}为一个对象 ,数据要指定类型 cmovies:Array cmovies:{type:String,default:"",required:true}
还支持 String ,Number,Boolean,Array,Object,Date,Function,Symbol 可指定多个数据类型
默认值为 obj 或者 Arr 时需用 factory function return 原理一样
required:true 必须要用 data 从父传过来,otherwise error
还可以自定义类型,cmovies:Person funtion Person(){}
72 因为 html 的属性不区分大小写,所以 子组件 cMessage 写在属性应该写 c-message
73 子传父 ,自定义事件 this.\$emit("itemclick",item) 发射自定义事件,还有对象 item 给父组件


75 avoid 直接修稿父组件传过来的值,用一个变量来保存,再双向绑定,或者直接@input 修稿父组件 data
每一次 snum1 重新渲染, input 也会重新获取绑定的值,并不是重新渲染,所以造成我一改变 input 框里的值,因为 snum1 的 render,input 又重新绑定回 ssum2 的值,ssum2 的值只获取一次
要么直接v-model=""绑定ccmessage 要么绑定cmessage 发送改变message
watch:{ccmessage(newValue,oldValue){this.$emit("req",newValue)}}当监测到数值的改变时,进行opera
76 在 par component 操作 son 通过 this.$children 拿到子组件的对象数组  this.$children[index].methods
不同得组件,或者相同的组件复数,都会添加到子组件的对象数组  
 $childrent 用的比较少,因为取决于下标值,easy to change
$refs 给组件起属性名 ref="" this.$refs 是一个对象,会把ref=""的value 添加进对象的key,组件作为value
  77this.$parent. 当父组件为实例时,或者全局注册时,$parent即为Vue实例,否则为父组件
  78 不能直接使用被嵌套的组件 如cpn2中的cpn1  this.$root 直接访问根组件,即实例
79 slot 插槽 let component have extend usage method template 中 预留 pre <slot name =""></slot>自定义的写在组件中 slot 可以有默认值 默认替换时回替换掉所有无 name 属性的 slot=""具名插槽 name="clc"
80 编译作用域 模板的作用域在组件中 ,模板实例的作用域在实例 vue 中
81 $refs, $children 是创造出来的对象,无法在初始进行数据绑定和计算
83 作用域插槽的使用,在模板实例中使用组件中的数据,1 在 slot 标签中(模板中) 通过 v-bind:变量="data" 2.在 div 中 slot 标签之间替换 插入一个<template></template> 2.5.2 以上可以用 div ,
添加一个属性 v-slot/slot-scope="slot(任意)"创建出一个对象 slot,数据在这个对象中
84aa join("-") 把一个数组一"-"拼接, 并且以字符串的形式返回
84 code 量大带来的问题,变量名容易重复 ,可以大的匿名函数包裹(function(){})()
es5 方法,整个文件放在一个匿名函数中,将匿名函数中的变量,函数都保存在一个对象中


85 commonJS 的导出 语法在 aaa.js 文件 module.exports={ flage:flag } 通过底层 parse node 环境可以用
var aaa =require("./aaa.js") var flag =aaa.flag  
 对象的解构 var {flag,sum}=require("./aaa.js")
86 es6 的导出 1 直接 export const clc=1 2 最后 const clcl export {clc}
export default import 起名 不用括号 from ""
import *as clc from"./aaa.js" 把所有的导出都 save 到 clcobj 中
本身是不支持的,但是添加了 type="module"后,浏览器作文底层  支持es6
87webpack 现代化的 javascript 静态模块打包工具 处理模块化的依赖关系
common tools grunt/gulp/webpack/rollup
88 只能做简单操作,不能使用模块化管理 grunt/gulp
89 webpack 配合 common js 模块化开发思路, distribution src 两个文件夹
src 放开发的 development 的 js js 中的 module 采用 comonjs 语法,然后采用 webpack 来打包生成 bundel.js
webpack 会自动处理模块之间的依赖
90 创建一个 webpack.config.js module.exports={entry:"",output:{path:"绝对路径/动态",filename}}
因为要依赖 node 相关的东西 ,用指令 npm init 再用 npm install
导入一个对象 const path = require("path") path.resolve(**dirname,"dist") **dirname 全局上下文对象  
 91 映射 webpack 指令 为 npm run
92 要在本地文件夹装一个 webpack 开发时依赖,运行时依赖 只是在开发需要 装的时候加一个终端命令
npm install webpack@3.6.0 --save-dev 指令打包的一个优点,优先在局部找对应的 webpack
93 loader 加载 css 图片 es6->es5,scss,less->css 要用 webpack 的拓展 loader require(csspath)
css-loader 只负责 loadercss 文件 ,style-loader 将模块的导出作为样式添加到 DOM 中 读取时从右向左 先读取再添加
94 less 文件 npm install --save-dev 1.less-loader 2.less 加载器,css 转换器 同理
95 url loader limit: 8192byte 当图片的大小 kb*1024 小于 limit 会将图片编译成 bae64 字符串形式直接保存在文件 bundle.js 文件中,不需要用另外一个文件来 save, 大于的时候回采用另外一个 loader file loader,会把图片打包到 dist file 中一起发送到 serve,用哈希算法防止命名重复自动生成名字
在 config 采用配置 publicPath"" 规定所有已经解析的文件目录，url 相对于 index.html。
实际项目不用,因为项目会自动把index.html转化到dist文件夹
96 name:"img/[name].[hash:8].[ext]" 更改命名规范,config limit 下的 name 文件夹 img/[原来的名字].
97es6->es5 loader npm install --save-dev babel-loader@7 babel-core babel-preset-es2015,配置要改
98 配置 vue npm install vue --save import Vue from "vue" 引入依赖
99 Vue 在构建的时候有两类版本, runtime-only(代码中不能有 template) runtime-complier
100 使用完整版，则需要在打包工具里配置一个别名 resolve: alias
101 template 的内容会替代整个 el 挂载的 div template: "<cpn1/>", 定义组件抽离模板
102 把 cpn1 从另外一个 js 文件匿名导入
103 npm install --save-dev vue-loader vue-template-compiler 安装 vueloader 就可编译 compiler 文件
记得要配置, 版本太高要一个 plugin 插件,降低版本 npm install upgrade 13.0.0
104 在 resolve 下添加 extensions:[".js",".css"]导入时即可省略
105 vue 官网查 webpack alias 'vue\$': 'vue/dist/vue.esm.js'
106 小心 import 和 require 混用 js 文件中混用 require 和 export 但是不能混用 import 以及 module.exports

107 Plugin bannerplugin const webpack = require('webpack');
plugins:[new webpack.BannerPlugin("版权归 clc 所有")] 自带的插件
108 打包 html 的 plugin htmlwebpackplugin npm install html-webpack-plugin --save-dev 3.2.0
会自动在导出路径生成 index.html 文件,可传入一个参数模板
109 js 压缩 plugin npm install --save-dev uglifyjs-webpack-plugin@1.1.1
110 搭建本地服务器 基于 node.js 内部使用 express 框架 是一个单独的模块
npm install webpack-dev-server@2.9.3
这个框架会 serve 某个文件夹 实时监听内容的改变, if change recompiler ,在 ram 中 test
111 cli 2 ->webpack @3.6.0. ->dev-server 2.9.3
112 devServer:{contentBase:"./dist",inline:"true,port :指定端口号"  
 } --open 运行后自动打开  
 112 安装时 -g 全局安装
113 webpack-配置文件的分离,把开发版本和生产版本的配置文件分离
npm install webpack-merge
114 const webpackMerrge = require("webpack-merge"),
const baseConfig = require("./base_congif")
module.exports=webpackMerrge(baseConfig,{}) 合并两个文件
115 --config ./config/dist_config.js npm 后添加
116 Vue Cli 大型项目必须使用 考虑代码目录结构,项目结构和部署,热加载,单元测试 太多效率低
Cli command line interface 命令行界面
117 npm install -g @vue/cli
118 安装 拉取脚手架 2.x 版本 npm install -g @vue/cli-init
119 cli2 初始化项目 vue init webpack my-project
cli 3 vue create my-project
120 切换镜像 npm install -g cnpm --registry=https://registry.npm.taobao.org
121 runtime-only 体积小 ,效率高
122 node 使用 C++写的,基于 chrome V8 引擎 js->字节码->浏览器 js->二进制代码 chrome
123 build webpack 相关的配置 node_modules 依赖 node 的模块 src 开发地方
static 静态,原封不动 save in dist .babelrc es 代码转化的配置
.editorconfig 项目文本 相关配置 .gitignore git 仓库忽略的配置
.postcsssrc.js css 相关转化的配置
124 版本 ^ 4.20.x ~4.x.y 大于这个版本
125 vue template compiler proces 保存在 options 中 ->解析成 ast(抽象语法树)abstract syntax tree
->vue options 中的 render 函数 ->virtual dom-> ui
126 runtime -only render ->vi dom-> ui
127 runtion-compiller tem->ast->vdom ->dom
128 render:function(createElement){return createElement("div",{class:"box"},["<h1>123</h1>"])}
标签 ,属性 ,content 内容,可以嵌套使用
第二种用法 template: '<cpn1/>' == render:function(createElement){return cre...(cpn1)
}
129 .vue 文件中的 template 是由 vue-template-compiler parse 的,导入的 App 对象已经被解析完毕,
从.vue 文件出来的对象无 template
130 vue clo3 cli 2 的区别, cli3 是基于 webpack4 打造,cli2 基于 webpack 3
cli3 是 0 配置,无 build 和 config 配置, 提供了 vue ui 命令,提供了可视化配置,
131 mannually select feature 手动选择要素 .rc run command
133 public cli2 的 static .browserslistrc 市场份额,最后两个版本 ,否定
134 vue-cli-service 管家,
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

Ajax请求  asynchronous javascript  and xml
网速慢时,加载时间慢,页面一刷新,所有内容消失,页面跳转又要重新刷新页面,资源浪费
application:上拉加载,列表切换,表单验证,搜索提示,网站环境才能生效
不用刷新页面即可与服务器通讯的方法还有:1Flash 2.java applet 2框架 3flame 4xmlhttprequest 
客户端(xhtml,css,js)<->传输(协议:xmlhttp,载体,文本txt,xml,json)<->服务器端(php,等)
noedmon app.js
var xhr = new XMLHttpRequest();创建ajax对象 设置请求地址和方式xhr.open("get","url")发送请求
xhr.send,响应时自动调,xhr.onload=function(){xhr.responseText}

 <script>
xhr.responseText 返回的数据都是JSON字符串
本地服务器搭建  const express = require("express")const path  = require("path")
const app = express(); app.use(express.static(path.join(__dirname,"public")))
app.listen(2333)app.get("/first",(req,res)=>{res.send({name:"chenlicheng",age:18})})
服务器内的文件要在服务器内的路径  localhost:2333默认打开的是localhost:2333/index.html
Js有一个对象 JSON.parse() 转换成对象 JSON中属性名必须加双引号,不能为单引号
form 表单的get()效率高,隐私暴露 和post 隐私性高
ajax get 请求xhr.open("get","http...info?name=chenlicheng&age=18") xhr.send()
post 请求 xhr.setRequestHeader("Content-Type","application/x-www-form-urlencoded")
xhr.send(name=chenlicheng&age=18)
报文 传递的数据块 传送的数据和一些附加信息,这些数据要遵循一些格式
使用模块const bodyParser =require("body-parser") app.use(bodyParser.urlencoded())
就可以通过res.body访问请求体内的内容
application/x-www-form-urlencoded 对应name=chenlicheng&age=18格式
"application/json" 对应的js对象的JSON格式  JSON.stringify(obj)
xhr.send(JSON.stringify(data))
app.use(bodyParser.json()) 安装插件的时候换成json  req.body  req.query
无论服务器发送什么,只有执行了res.send(),静态才能执行onload=()=>{}
ajax 创建,配置,发送请求,接受数据响应都会对应一个ajax状态码
0请求了但未初始化,即未调用open(),1已初始化未发送 2 已经发送未响应 3正在接受响应4响应完成
获取ajax状态码 xhr.readyState()  xhr.onreadystatechange()当ajax状态码变化时触发,会不断的回调
onready 虽然兼容ie低版本,但是调用多次,效率低
获取http的状态码 xhr.status    res.status(400).send("err  or")访问/error路由时,返回错误响应
HTTP status  200 OK 404 not found服务器接收不到  400 bad request返回结果不是预期结果
500服务器端出错  网络中断 ,会触发xhr下的onerror 事件
ajax状态码 ajax请求的过程,请求发生到哪一步 ajax对象返回的
 http status 请求的处理结果  服务器返回的
 const fs = require("fs")  fs.readFile("./text.txt",(err,result)=>{res.send(result)})
 node环境操作txt文件   
 解决低版本ie auto cache 问题,当请求的router与原来相同时,会从缓存中提取,只需拼接math.random()
 随机生成0到1的query即可    ajax同步异步 本身就是异步操作或者加上/?time=+new Date()时间蹉
 截取query    query=query.substr(0,query.length-1)  Date.parse(new Date())
const contentType = xhr.getResponseHeader("Content-Type") 获取响应头返回的数据类型
contentType.includes("application/json")  在为true
Object.assign(defaults,options) 覆盖默认值
art-template 的实现 模板引擎
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


Vuex vue.js的状态管理模式, 集中式存储管理,  也集成到Vue的官方调试工具devtools extension 提供了零配置time-travel,状态快照导入导出高级调试功能
单个页面的状态管理  action->state->view->action
Vuex 的配置import Vue from "vue"import Vuex from "vuex"Vue.use(Vuex)
const store = new Vuex.Store
({state:{},mutations:{state,payLoad},actions:{context,payload},getters:{state ,getters},modules:{}})
common 放在 state  通过$store.state.访问
vue components->actions->mutations->state->vue component
Devtools vue开发的浏览器插件  记录修改state的状态  是在Mutations这个步骤进行记录,如果直接通过$.store.state改变 状态,Devtools将会跟踪不到  可以跳过actions  ,mutations进行同步操作
actions -> Backend api 后端api  async  
mutations 中的方法会默认传入state 或者通过this.state访问,触发事件通过this.$store.com("mutations")
State 单一状态树  Single Source of Truth 单一数据源  资源统一集合到一个store中
Getters  ?= computed   Getters 中的方法可以有两个params state ,getters  
getters  属性后面加()自定义决定返回,  通过getters返回一个函数  store.getters 暴露
Mutation Vuex.store upgrade 更新的唯一方式 提交summit mutation   分为两部分,commit 字符串的事件类型,this.$store.commit("change",num) 可以传递一个num值   Payload  负载 载荷可以为str,obj
一个回调函数handler  第一个参数为 state  第二个参数为commit过来的value  
一个是getters显示的时候传参,一个是mutation事件传参
/使用计算属性连接vuex的变量，在用watch去监听，变相的实现监听vuex内部state变化
commit("str",num)=commit({type:"str",num:num})     mutation中改为payLoad
state 中的属性attr对应一个Dep观察者模式,Dep->[watcher,watcher]每一个attr的展示就是一个watcher,通过Dep更改watcher,初始化的属性会被加入到响应式系统,而响应式系统会监听属性的变化,当属性改变时,会通知界面的所有watcher,进行刷新,后添加的不会加入到响应式系统,很多都能响应,唯独直接通过索引修改数组/对象不行,可通过 Vue.set(arr/obj,index/key,"value")  delete key 不能响应式  Vue.delete(arr/obj,key/v)
growUp(){}==["growUp"](){}==[常量](){} 函数名的替代
mutations 中进行async 异步操作devtools无法catch  所以要加多一步action ,$store 就是new 的实例
有两个方法 commit,dispatch  通过dispatch("事件类型"),在action(参数都带有context)中异步操作发送 commit(),在mutation中进行改变,dispath与commit一样有直接还有对象形式的提交风格context.commit
意思就是让异步操作通过Promise优雅,在dispatch中调用 调用dispatch可以获得对应事件类型的返回值
modules:{moduleA,moduleB},const muduleA={state:,mutation.......}
把通过$store.state.moduleA.message  把modulea的state添加到state中,其余的$store.getters.event相同,会自己去找  模块中的getters(state,getters,rootstate) 多了一个根state
module中的action中的context是很大的对象,包含commit,dispatch,getters,rootGetters,rootState,state
actions 中的context (context)可写成({state,commit,rootState}) 还有一些其他的,可取可不取
对象的解构 const obj = {name:"why",age:18,height:1.77} const {name,age,height}=obj
数组的解构 const names=["why","clc","wjp"] const [name1,name2,name3]=names
结合Promise 的异步Vuex的优雅写法    this.$store.dispatch(INCREMENT).then(res => {this.$store.commit("up");console.log("我已经完成了");});

axios  ajax i/o system 是一个基于 promise 的 HTTP 库
1.传统XHR,rubbish2.$ajax 冗余3,vue-sourece stop upgrade4 axios
axios(confing),axios.request(),axios.get() .delete  .head .post  . put .patch
axios({url:"http://localhost:3000/axios",baseURL,tiemout,method:"get").then(res=>{console.log(res);})
axios结合promise的使用  get请求可自行拼接,也可 params:{type:"pop/sell",page:1}
"http://152.136.185.210:8000/api/n3     recommend/(home/data) "type="pop& age=1
axios.all([axios({}),axios({})]).then(result=>{})  /.then(axios.spread((res1,res2)=>{}))
axios的全局配置  axios.default.baseURL=
实际上的服务器请求时通过代理服务器nginx,分布式自动分发
创建对应的axios的实例
const instance1 = axios.create({baseURL:""})  instanece1({url:""}) 不用全局的axios({})
axios的模块封装,防止对某种模块的依赖太大,将其进行独立封装,
instance.interceptors.request.use(config=>{return config},err=>{}) 拦截config操作,显示动画,拦截登录,跳转其他界面,让用户携带信息token
instance.interceptors.response.use(res=>{return res},err=>{}) 

一般许可证选择MIT
1创建仓库 ,git-clone 复制粘贴,除了 .git文件,git add. git commit -m "#" git push
2创建 git remote add origin url

supermall
项目的划分
->src
assets/[css|img]  components/[common|content] 放公共的组件  views  放大组件 router   store  network    common/const.js
normalize.css   css中  :root{}获取根元素html  
在css中定义变量 --large-size:50px; 使用  font-size:var(--large-size:50px)

cli4中别名配置的坑 html中使用要加~ css中使用要加~
@在cli3/4中已经默认是相当于__dirname拼接上,src 就是src,不能再定义不然冲突
path.join(__dirname,dir)  path.join(__dirname,"..",dir) 拼接上..会把最后一个路径切掉
publice 下的 icon  index <link rel="icon" href="<%= BASE_URL %>favicon.ico">
函数调用,压入函数栈(保存函数调用过程中的所有变量)
函数调用结束->弹出函数栈(释放所有的变量)
变量res在栈中保存着堆的指针,函数结束,指针回收,堆内的数据打上垃圾回收标签
@touchstart @touchmove @touchend  针对移动端的事件
this.message 数据可以不用初始化直接在方法或者等使用
cloneNode() 拷贝一个节点 传true 递归复制子孙节点,否则只复制当前节点

float浮动,positon定位,通过设置left,right移动,通过分段移动制造动画
通过flex布局,通过css3进行动画移动,transition

 flex-shrink  flex-items不会撑大flex-container 的大小,默认会执行flex-shrink的收缩,当flex-shrink=0时,不收缩,多出的算溢出
原生js在移动端scroll会卡顿,不建议使用

注释,分布,布局要在写代码的时候就complete,
position: sticky;top: 44px; 吸顶效果 
切换,判断index==currentindex
const page = arguments[1]?arguments[1]:1 通过判断argument设定默认值 es6可直接赋值
const page = arguments[1]||1
const a=a.concat ===   a.push(...[arr])  ...会把数组解析添加

两种思路,内容由编辑者决定时,将v-for作为插槽插入,当内容展示为数据库的数据时,将内容传递到子组件中展
原生部分面积滚动, 定高度, o'ver-flow scrooly

Bscroll
better-scroll 滚动 import BScroll from let wrapper = document.querySelector('.wrapper')let scroll = new BScroll(wrapper)  wrapper>只跟一个整体的content
 const bscroll=new BScroll(document.querySelector("#catalog"),{probeType:2})
bscroll.on("scroll",(position)=>{console.log(position);})
probeType 01不监测,2以上监测,3监测惯性
pullUpLoad:true     bscroll.on("pullingUp",()=>{console.log("我到达了底部");}) 监听事件
exe bscroll.finishPullUp()完成第一次监听
ref=""不止可以用于子组件,还可以用于查找某个元素对象,dom,找当前页面的某个对象
height: 100vh;viewport height 自动算成视口高度 
 calc(100% - 49px);  高度计算 切记要加空格隔开 1自动计算高度.2绝对定位
 .native修饰符,监听组件实例的点击
 scrollTo(0,0,500),
 解决betterscroll 在图片渲染之前提前计算好content高度的问题
 原生js listernr 图片 img.onload=function(){}
 vue中@load = "event"
 1.每一次图片加载完成,发送commit修改vuex中的,state,把state数据绑定给一个计算属性,再监听计算属性的改变,进行刷新refresh() 重新计算高度
 事件总线  Vue.prototype.$bus= new Vue() this.$bus.$emit("imgLoaded")this.$bus.$on("imgLoaded",()=>{console.log("我监听到了你的变化");})
 把发出的函数用一个变量保存起来,
 this.$bus.$off("imgLoaded",函数变量名)
 @input  value 改变就触发  @change  失去focus触发
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

部分混入 const mixin={mounted:()=>{}}  然后在组件内选项 mixins: [mixin]
生命周期的函数可以抽,会合并,方法内的函数不会合并,会覆盖
crated之前初始化部分二层结构的数据, mounted只是挂载el,但是并不一定渲染完成,渲染需要一定的时间,
this.nextTick保证渲染完成,但是图片不一定加载好

arrs.find((arr)=>{return })  会按照顺序吧arr中的按顺序传入,满足return这个arr
import { mapGetters } from 'vuex'  ...mapGetters函数,将getter混入computed
...mapGetters(['doneTodosCount','anotherGetter',// ...]) 映射
...mapGetters({lenght:"doneTodosCount"}) 起别名  在computed中注册
forEach  filter  map reduce
import{mapActions} from    在methods中 ...mapActions([""])使用的时候要加this
  top: 50%;left: 50%;transform: translate(-50%,-50%);根据自身的比例来居中fixed  
  export default obj ,Vue.use(obj)  触发obj.install=(Vue)=>{}

  FastClick  解决浏览器自带的wait 300ms delay to check if enlarge
  npm install fastclick import FastClick from "fastclick"  FastClick.attach(document.body)

  vue-lazyload import VueLazyLoad from "vue-lazyload" Vue.use(VueLazyLoad,{loading}) v-lazy

  css 单位装换为 vw  vh
  postcss-px-to-viewport   iphone 6设计稿 (750×667)

  linux->centos->nginx

  响应式原理  把对象传进vue时,创建Observer new Observer 响应式系统
  把data数据forEach遍历,通过Object.defineProperty(obj,key,{
    set(newValue){},get(){}}), 给每一个数据创建一个dep,dep1,dep2,当value发生改变时,会触发set(newValue)方法中,获取访问obj.key,会触发get方法,当使用这个数据时,在get中 dep,在哪里使用了这个数据,就给他创建分发一个watcher,触发dep中ed添加sub[]数组方法把watcher 添加到类Dependency中的 subscriber数组,在set方法中,当数据放生了变化,触发dep.notify方法,depnotify会遍历数组中的watcher,并且触发watcher中的一些方法
    name->Dep>subscriber->[watcher1watcher2,]

# v-slot=""的速写属性
PascalCase 大驼峰
camelCase 小驼峰
kebab-case 短横
组件的 data 必须是一个函数
单文件组件的文件名应该要么始终是单词大写开头 (PascalCase)，要么始终是横线连接 (kebab-case)。
和父组件紧密耦合的子组件应该以父组件名作为前缀命名。|- TodoList.vue|- TodoListItem.vue└─ TodoListItemButton.vue
在单文件组件中没有内容的组件应该是自闭合的。能单闭合则单闭合
在声明 prop 的时候，其命名应该始终使用 camelCase，而在模板中应该始终使用 kebab-case。
Props 顺序  标签的 Props 应该有统一的顺序，依次为指令、属性和事件。
export default {
  name: '',
  mixins: [],
  components: {},
  props: {},
  data() {},
  computed: {},
  watch: {},
  created() {},
  mounted() {},
  destroyed() {},
  methods: {},
};

动态渲染img要用item?require()



