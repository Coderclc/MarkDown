# ADMIN

## tips

stage 线上环境的测试环境版

```
import AppMain from './AppMain'
export { AppMain }
export { default as AppMain } from './AppMain'
```



## Details

view和api file 对应

router-view 当组件复用切换时不触发create,mounted, bind key solve

svg-icon 会成为主流方式

## 多环境

"build:prod": "NODE_ENV=production node build/build.js", 

 "build:sit": "NODE_ENV=sit node build/build.js",	

在全局变量process.env中

var env = process.env.NODE_ENV === 'production' ? config.build.prodEnv : config.build.sitEnv

## 权限验证

### 登录

当用户填写完账号和密码后向服务端验证是否正确，验证通过之后，服务端会返回一个**token**，拿到token之后（我会将这个token存贮到cookie中，保证刷新页面后能记住用户登录状态），前端会根据token再去拉取一个 **user_info** 的接口来获取用户的详细信息（如用户权限，用户名等等信息）。

权限验证：通过token获取用户对应的 **role**，动态根据用户的 role 算出其对应有权限的路由，通过 **router.addRoutes** 动态挂载这些路由。使用vuex管理路由表，根据vuex中可访问的路由渲染侧边栏组件。

一个是能否进入,一个是侧边渲染

为什么不采取路由表由后端根据用户动态生成?前后端不分离,

### Cookie

第一次访问,服务器会返回cookie,在response  head Set-Cookie 中,第二次访问会携带cookie,在request head中

有效期默认为一个会话

非同源时携带cookie,前后端axios koa 都要设置 withCredentials:true

出于安全考虑,跨域请求都会发送两次请求,第一次为OPTIONS方法发起一个预检请求,

可设置Access-Control-Max-Age:60\*60\*24取消预检请求

### Session

与cookie保存在客户端浏览器不同,session状态保存在服务器中,当客户端访问服务器时,服务器会生成session对象,对象保存的是key:value值,服务器会将key传回给client的cookie,第二次访问,服务器会将key传回给server,server返回value

## Webpack

config configureWebpack name 打包时才能正确插入标题

## Process

process.env.port  命令行控制端口   set port=8081 yarn dev   //   yarn dev --port=7777

process.env.npm_config_port  全局变量控制端口

## VueCli

先读取.env.development  -> .env -> vue.config.js 

.env.production比.env优先且不会被覆写

.env.development设置的变量全部会加到process.env变量中

yarn dev  --mode production可通过mode更改默认环境

yarn dev 即 vue-cli-service serve   process.env.NODE_ENV === 'development' 设置了全局变量

yarn build:prod   process.env.NODE_ENV === 'production'  设置了全局变量

stage 预发布环境

publicPath 如果站点部署到子路径下需设置为/admin

configureWebpack name 打包时才能正确插入标题

outputDir:输出的文件夹

assetsDir:"static"静态文件夹单独抽离

lintOnSave: process.env.NODE_ENV === 'development' 开发环境下每次保存都lint代码

productionSourceMap true时生成.map文件可定位报错位置,但打包的文件大很多

devServer :

1.port 端口      2.open 浏览器自启 

3overlay 默认false {warnings: false, errors: true }全屏覆盖报错

4 .before   服务器内部执行中间件之前执行自定义中间件 before(app) {

app.get('/login', function(req, res) { res.send('hahah') }) }

 解析 "application/json"       app.use(bodyParser.json())

 解析 application/x-www-form-urlencoded    app.use(bodyParser.urlencoded({  extended: true }))

extended: true：表示使用第三方模块qs来处理

extended: false：表示使用系统模块querystring来处理，也是官方推荐的

process.argv  返回一个数组，其中包含当 Node.js 进程被启动时传入的命令行参数

1. Node.js 进程的可执行文件的绝对路径名
2. 正被执行的 JavaScript 文件的路径
3. 其余的元素是任何额外的命令行参数 eg --preview

--preview read .env.production config

.travis.yml 是travis自动部署的配置文件

const { errorLog: needErrorLog } = settings 改名字

## Svg

symblo  是未来的主流

svg-sprite 解决svg按需加载[svg-sprite-loader](https://github.com/kisenka/svg-sprite-loader) ,将js文件的样式js-cpn use  变成svg-cpn

自动导入  webpack 的require context

svgo 将svg 冗余的信息剔除,会导致多色icon无法使用

## Sortable

或者[Vue.Draggable](https://github.com/SortableJS/Vue.Draggable)

## chokidar

Node.js 提供fs.watch和fs.watchFile用于处理文件监控.但有以下问题

1. OS X系统环境不报告文件名变化
2. OS X系统中使用Sublime等编辑器,不报告任何事件
3. 经常重复报告,多数事件通知为rename,不能简单的递归监控文件

```
const mockDir = path.join(process.cwd(), 'mock') //cwd()执行文件的绝对路径

module.exports = app => {
    chokidar.watch(mockDir, {
        ignored: /mock-server/,
        ignoreInitial: true //default false,捕获add/addDir 事件
    }).on('all', (event, path) => {
        console.log(event);  change/add/unlink
        console.log(path); 路径
    })
}
```

## Mock-server

```
 devServer: {
    port: port,
    open: true,
    overlay: {
      warnings: false,
      errors: true
    },
    before: require('./mock/mock-server.js')
  },
```

启动本地服务器之前先执行一个函数,传入app  基于app= express()

mock-server.js  创建接口

index.js 	整合所有路径对象, 开发mockserver搭建

user.js......

app.url正则表达式匹配多个路径  res.json()返回json数据格式

注册的接口都 按顺序依次加入到app._router.stack对象中 ,默认有0~11 12 个元素

node.js 清楚require.cache 缓存 因为require的缓存机制,在第一次调用require时即缓存下来,无法hot更新require.cache是一个对象,键为文件路径

require.resolve 查询某个文件的完整绝对路径

## 按钮级别权限控制

使用指令来实现少部分

## 侧边栏

hack法 不断的改变url中的query

## Dialog

直接将值赋值给dialog 内外问题,

```
//赋值对象是一个obj
this.objData=Object.assign({}, row) //这样就不会共用同一个对象

//数组我们也有一个巧妙的防范
newArray = oldArray.slice(); //slice会clone返回一个新数组
赋值以后重新指向新的引用
```

## Tabs

可用  <keep-alive> 缓冲 el-tabs挂载

## Select 

[vue-multiselect](https://github.com/monterail/vue-multiselect) 解决bind  obj  回显问题

## 富文本

tinymce  ckeditor

## Markdown

[simplemde-markdown-editor](https://github.com/sparksuite/simplemde-markdown-editor) 

转换库[showdown](https://github.com/showdownjs/showdown)

## 导出excel

csv比xlsx简单的多

创建一个a标签，写上`data:text/csv;charset=utf-8`头，再把数据塞进去，`encodeURI(csvContent)`一下就好了， [stackoverflow回答](https://stackoverflow.com/questions/14964035/how-to-export-javascript-array-info-to-csv-on-client-side)。

转xlsx使用[js-xlsx](https://github.com/SheetJS/js-xlsx)，

## echart

[gallery](http://gallery.echartsjs.com/explore.html)

## Postcss

 autoprefixer 只会对通过 vue-loader 引入的样式有作用，换而言之也就是 .vue 文件里面的 css autoprefixer 才会效果

解决方法

```
//app.vue
<style lang="scss">
  @import './styles/index.scss'; // 全局自定义的css样式
</style>
```

修改配置修改postcss.config.js即可 ,配置与 [postcss](https://www.postcss.com.cn/)相同

​    *// to edit target browsers: use "browserlist" field in package.json* 编辑目标浏览器

```
"browserslist": [
    "> 1%",兼容全球使用率大于1%的游览器
    "last 2 versions",
    "not ie <= 8"
  ]
```

## Vue Cli3

vue inspect > output.js  默認生成的是開發環境的配置

vue inspect --mode production > output.js

## redirect 

在不刷新页面的情况下reload page

/redirect路由 重定向

## addRoutes && removeRoutes

官方api addroutes  但没有remove 否则会重复挂载  只能通过函数返回router重置reset 

reset 的是初始router中的matcher

## Mock 数据

拦截了所有的请求并代理到本地，然后进行数据模拟，所以 `network` 中没有发出任何的请求。但它的最大的问题是就是它的实现机制。它会重写浏览器的`XMLHttpRequest`对象，从而才能拦截所有请求，代理到本地。大部分情况下用起来还是蛮方便的，但就因为它重写了`XMLHttpRequest`对象，所以比如`progress`方法，或者一些底层依赖`XMLHttpRequest`的库都会和它发生不兼容

## async/await or promise

```
getInfo()
  .then(res => {
    //do somethings
  })
  .catch(err => {
    //do somethings
  })
  
 try {
  const res = await getInfo()
  //do somethings
} catch (error) {
  //do somethings
}
```

try catch 使await 得不偿失  单个使用then

await Promise.all

```
const foo = () => {
    return new Promise(resolve => {
        setTimeout(() => {
            resolve()
        }, 2000);
    });
}
async function bar() {
    await foo().then(res => {})
}

Promise.all([bar(), bar()]).then(res => {
})
Promise.all([foo(), foo()]).then(res => {
})
```

then()的返回值就是promise所以then().then()

Promise.all()捕获

1.  return  new  Promise  resolve()
2.  getUserinfo().then()的返回值就是promise   所以直接 return  getUserinfo().then then 会自动return  ''
3.  async    await   getUserinfo().then() 等待执行完毕  ,async  函数会自动返回一个空的promise

```
const foo = () => {
	return new Promise(resolve => {
		setTimeout(() => {
			resolve('')
		}, 2000);
	});
}
1.
 function bar() {
	return new Promise(resolve => {
		foo().then(res => {
			resolve()
		})
	});
}
2.
 async function bar() {
		await foo().then(res => {
		})
}
3.
function bar() {
	return foo().then(res => {})
}


Promise.all([bar(), bar()])
	.then(res => {
		console.log(res);
	})
```

## 命名规范

- 所有的`Component`文件都是以大写开头 (PascalCase)，
- 所有的`.js`文件都遵循横线连接 (kebab-case)。
- 在`views`文件下，代表路由的`.vue`文件都使用横线连接 (kebab-case),代表路由的文件夹也是使用同样的规则。

## Cdn

https://juejin.cn/post/6844903840626507784

## watch

immediate 初始化加载  deep  深度监听

深度监听表单变化

## $attrs 和$listeners

attrs 为未经过prop绑定的属性\

## computed

 created(){return form.created}

使用get 和set  ,表单组件直接绑定 created 改变时间戳

还有如果input绑定的值时vuex直接修改会报警告,建议使用set  commit改变

## Object.freeze

this.item = Object.freeze(Object.assign({}, this.item)) 将data的值对象冻结,减少开销

当你把一个普通的 JavaScript 对象传给 Vue 实例的 data 选项，Vue 将遍历此对象所有的属性，并使用 `Object.defineProperty` 把这些属性全部转为 `getter/setter`，它们让 Vue 能进行追踪依赖，在属性被访问和修改时通知变化。 使用了 `Object.freeze` 之后，不仅可以减少 `observer` 的开销，还能减少不少内存开销。相关 [issue](https://github.com/vuejs/vue/issues/4384)。

## Functional

 函数式组件,比如能用`v-show`的地方就不要用`v-if`，善用`keep-alive`和`v-once`，`Object.freeze()`处理 [vue big data](https://github.com/vuejs/vue/issues/4384) 问题等

## 性能优化技巧

 JS 引擎是单线程的运行机制，JS 线程会阻塞 UI 线程，所以当脚本执行时间过长，就会阻塞渲染，导致页面卡顿。 `script` 执行时间短，所以它的性能更好。

[vue-9-perf-secrets  ](https://slides.com/akryum/vueconfus-2019#/)  [掘金](https://juejin.cn/post/6922641008106668045#heading-2)

1. Function components 

   大量复用的没有响应式数据的子组件采用 函数式组件函数式组件和普通的对象类型的组件不同，它不会被看作成一个真正的组件，我们知道在 `patch` 过程中，如果遇到一个节点是组件 `vnode`，会递归执行子组件的初始化过程；而函数式组件的 `render` 生成的是普通的 `vnode`，不会有递归子组件的过程，因此渲染开销会低很多.因此，函数式组件也不会有状态，不会有响应式数据，生命周期钩子函数这些东西。你可以把它当成把普通组件模板中的一部分 DOM 剥离出来，通过函数的方式渲染出来，是一种在 DOM 层面的复用

2. child component splitting

   把这个耗时任务 `heavy` 函数的执行逻辑用子组件 `ChildComp` 封装了，由于 Vue 的更新是组件粒度的，虽然每一帧都通过数据修改导致了父组件的重新渲染，但是 `ChildComp` 却不会重新渲染，因为它的内部也没有任何响应式数据的变化。所以优化后的组件不会在每次渲染都执行耗时任务，自然执行的 JavaScript 时间就变少了。 减少了重新渲染的组件

3. local variables

   大量重复操作this的时候,先缓存为局部,computed 默认传了this进来

4. reuse dom with v-show 

    使用 v-show代替v-if

5. keep-alive 

   空间换时间,占用内存缓存

6. deferred features 

   使用了 `Defer` 这个 `mixin`分批渲染

7. time slicing  

   当script执行时间过长的时候会有卡死的可能

8. non-reactive data

   ```
   const data = items.map(
     item => ({
       id: uid++,
       data: item,
       vote: 0
     })
   )
   object  key为响应式,增加了开销,当数据量大时延迟script 开销
   ```

   ```
   const data = items.map(
     item => optimizeItem(item)
   )
   
   function optimizeItem (item) {
     const itemData = {
       id: uid++,
       vote: 0
     }
     Object.defineProperty(itemData, 'data', {
       // Mark as non-reactive
       configurable: false,
       value: item
     })
     return itemData
   }
   
   ```

   类似的想要在上下文中共一个数据,并不一定要绑定在data上

9. virtual scrolling

之所以有这个差异，是因为虚拟滚动的实现方式，是只渲染视口内的 DOM，这样总共渲染的 DOM 数量就很少了，自然性能就会好很多。

虚拟滚动组件也是 [Guillaume Chau](https://github.com/Akryum) 写的，感兴趣的同学可以去研究它的[源码实现](https://github.com/Akryum/vue-virtual-scroller)。它的基本原理就是监听滚动事件，动态更新需要显示的 DOM 元素，计算出它们在视图中的位移。

虚拟滚动组件也并非没有成本，因为它需要在滚动的过程中实时去计算，所以会有一定的 `script` 执行的成本。因此如果列表的数据量不是很大的情况，我们使用普通的滚动就足够了。



## 减少全局操作

避免使用document全局选择器,使用this.$el 组件根节点 this.$ref.xxx.$el

全局性事件window.addEventListener一定要销毁

Vuex避免太多,如果不可避免可以采用动态注册,动态销毁

## event bus

关系尴尬组件this.$bus.$on  this.$bus.$emit  this.$bus.$off(  在on處off

## Sass 和 Js 之间变量共享

js 将变量传给sass  写内联  ,或者var 变量

sass 传给js :**export** {  theme: $theme; }

## 自动注册全局组件

当然你也不要为了省事，啥组件都往全局注册，这样会让你初始化页面的时候你的初始`init bundle`很大。你应该就注册那些你经常使用且体积不大的组件。那些体积大的组件，如编辑器或者图表组件还是按需加载比较合理。

## hook

替代destroyed  api：`$on('hook:xxx')`

@hook:mounted='doSomething' 监听子组件的生命周期

## Vue SSR

## SVG 

svg-sprite-loader 和url-loader衝突問題 使用 webpack 的 [exclude](https://webpack.js.org/configuration/module/#rule-exclude) 和 [include](https://webpack.js.org/configuration/module/#rule-include) 

## 动态路由配置

```
const map={
 login:require('login/index').default // 同步的方式
 login:()=>import('login/index')      // 异步的方式
}
//你存在服务端的map类似于
const serviceMap=[
 { path: '/login', component: 'login', hidden: true }
]
//之后遍历这个map，动态生成asyncRouterMap
并将 component 替换为map[component]
```

##  Git Hooks



## Tips

大部分问题都可以通过key和vue.nextTick 解决

## .sync

emit 渲染层立即刷新,逻辑层必须等待下一次刷新才发生改变

this.$nextTick 注意包裹范围

[...数组的深拷贝]

deepCopy 对象的深拷贝

this.$forceUpdate 执行update

缓存cpn data,并将其指向拷贝给this.$bus去改变

$bus的改变无法实时渲染

## Sort

arr.sort(x,y)  函数返回值  正数和0为不调换位置  负数为掉换位置   

x为后,y为前  x-y即 后大于前,升序,反之为降序

例如[1,2,3,4]  x为 2 3 4 y为 1 2 3 两两比较执行三次

若[1,2,4,3]  则比较完变化的直接比较前面比较过大小的

