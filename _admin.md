# ADMIN

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

svgo 将svg 冗余的信息剔除

## Sortable



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