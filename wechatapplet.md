# weChat appLet
<script>
双线程模型 逻辑层+渲染层,提高了管控性和安全性(沙盒环境运行Js代码,不 允许任何和浏览器相关的接口,比如跳转页面,操作dom)
页面布局   WXML wechat markup language
页面样式   WXSS
页面脚本   javascript WXS  wexinscript

App->pages->components(custom/built-in内置)

文件结构 1APP js,json.wxss 全局   2page js,json,wxml,wxss,页面 3components js,json,wxml,wxss 组件  

default  默认呈现的是app.json中 pages选项数组的第一个index.wxml

使用  mpvue miniprogram vue http://mpvue.com/   https://www.jianshu.com/p/6f8d74be3ff8
WEpy https://tencent.github.io/wepy/   
uni-app   

project.config.json  保存一些环境配置,方便移植开发
libVersion 小程序的版本

sitemap.json
允许被微信爬虫记录索引,被微信小程序中的搜索搜索到

APP.json
pages:注册页面 第一个为默认打开的
window:
tabbar


APP.js
判断小程序的进入场景(群聊,微信好友,二维码,pull list) 不同的场景场景值不同 ,进行不同的操作在onshow传入的options 下的scene,在onlaunch中也有options传入
监听生命周期函数 onLounch
全局共享数据
global data  在app.js 创建 对象 globalData:{name:"chenlicheng"}  在page.js通过const app = getApp() 获取app.json实例对象  通过app.globalData.name拿到数据

WXML  
所有默认值为false 的布尔属性,写上属性名即为true
绑定 bind 布尔值时要加mustache 不然"false" 为true
view ==div  <view> 是一个组件，会在页面上做渲染；<block>不是一个组件
text==span <text>\n可以换行<text>  decode,  space,  selectable
button  size=mini   type="" primary default warn  bindtap="" 或者bind:tap=""
template  defined name {{text}} 使用  is   slot data="{{key1:value1,}}"
<import src=""/>  模板单独抽离引入 不能递归依赖
<include src=""/>  include 可以将目标文件除了 <template/> <wxs/> 外的整个代码引入，相当于是拷贝到 include 位置,可以递归依赖require
image usually single tag  有默认尺寸空间 320×240  src="/" /为小程序的根路径
input 
scroll-view  scroll-x  scroll-y
wx:for="{{10}}" 遍历10次  wx:for="10" 当成字符串,遍历两次,变量需要用mustache 语法  并且会自动生成每一项,名为item,索引index wx:for-index="idx" wx:for-item="itemName"更改变量名
wx:key="" arr为static  "unique"任意   dynamic "*this" 即为item 需要item为唯一的字符串或者数字
wx:if="{{true}}" wx:elif="" wx:else  渲染与隐藏
共同属性  id class  style  hidden  data-*  bind*/catch*
mustache  new Date().toLocaleString()  实时时间  里面可使用三目运算符,通过切换 ()? ()来改变样式, class="{{}}" 

WXjs
Page({data:{}})
方法不用写在methods中,并且拿数据要通过this.data.
直接修改页面是不会发生重新渲染的,很多地方也会获取不到,eg AppData
要放在this.setData({count:this.data.count+1})中

Wxss
行内样式>页面样式>全局样式
commend:class  id el, 后代空格, ::after,::before
rpx   response pixel  相对单位,根据屏幕自适应
eg iphone6 750rpx =375px =750物理像素,1rpx =0.5px =1 物理像素,屏幕越大,rpx:px 越小
@import "./wxss/common.wxss";导入样式,分号结尾  绝对路径,相对路径
weUI 的引入 ,复制所有的js.wxml,wxss代码

Wxs  wexinscript
eg Vue 的html中可以直接使用各种函数,过滤器,是因为Vue的内部处理
在wxml中不能直接调用js 中的函数
限制:WXS不能使用js中定义的函数,也不能调用小程序提供的API,
优点,在ios上运行速度比js快2~20倍,在Android一样
<wxs module="name"> module.exports={}</wxs> 不支持es6
<wxs src="../../wxs/info.wxs" module="info" /> 通过wxs 的src导入,不能使用 / 要用相对路径
wxs 引入wxs  var tools = require("./tools.wxs") 相对路径 

小程序的双线程模型
宿主环境,微信客户端 执行了wxml,wxss,js 
渲染层[webview](wxml,wxss) 和逻辑层(jscore)js
界面渲染过程 先把wxml拿去逻辑层转换成虚拟dom js对象,再放回渲染层渲染
<view><view>a</view><view>b</view></view>
{name:view,children:[{name:view,children:[{text:"a"}]},{name:view,children:[{text:"b"}]}]}
当通过setDate发生数据变化,逻辑层产生新的js对象,进行diff算法,把差异应用到原来的dom上 ,这就是数据驱动的原理

小程序的启动流程
用户打开小程序->下载小程序,启动小程序,加载解析onloadparse app.json 注册 app.js 中的APP()执行生命周期,加载自定义组件代码,注册自定义组件, 加载解析pase.json渲染层渲染page.wxml,逻辑层注册page,执行page  

const err = new Error()  throw err

获取授权,wx.getUsetinfo 已失效,需要通过button点击授权,按钮事件默认会传一个对象 event,并且按钮设置两个属性
open-type="getUserInfo" 把bindtap 改成 binduserinfo
还可以用 open-data 组件展示用户信息  设置type="?"

对象中的扩展运算符(...)用于取出参数对象中的所有可遍历属性，拷贝到当前对象之中

event事件对象
property:type  timeStamp 界面创建到触发时间  detail
        target  currenttarge  事件冒泡时,currentrarget记录的是产生事件的对象,tar为触发的对象
        touches  changedTouches 记录多手指触摸 一个记录当前状态,一个记录变化的区别
通过 data-name="value"  传递数据 在event.target.dataset中 
 data-index={{index}} 很奇怪,这里可以传递遍历出来的index,但是wx:key={{index}} err
capture-bind:tap  bind:tap 事件捕获,会发生事件冒泡
capture-catch:tap  catch:tap   
当你触发最内测的点击函数时,会触发最外侧的事件捕获,然后一层一层向下捕获,再触发最内侧的点击函数,因为事件向上冒泡,再从内到外依次触发点击函数,当使用catch时,停止向下捕获,或者向上冒泡

Custom-components
文件夹components->文件夹my-cpn->
在使用pages.json "usingComponents": {"my-cpn":"path"} 组件json 配置 "component": true,
组件js 中 Component({properties: {},data: {},methods: {}})
组件之间可以相互嵌套,自定义组件不能起 wx- 名
在全局app.json 中配置 "usingCom" 可以全局使用组件
components 不能使用id ,属性,标签选择器只用类选择器
pages 使用标签选择器会对组件产生影响
在component({options:{styleIsolation:"isolated"}})默认值不会相互影响
"apply-shared" pages影响component  "shared" 相互影响
class="~red" ~引用page组件名为.red的样式  ^因为父组件为名red的样式
properties: {header:String,},<header=""> 传递数据    
header:{type:String,value:"default",observer:(newVal,oldVal)=>{}}} 两种写法
传递样式,page->style到components, style要set in page
components <class="addclass"> 父 addclass="red" 注意addclass 不能大写
并且要设置 externalClasses: ["addclass"]  类名不能与tag相同 不能大写
传递事件 this.triggerEvent("increment",{},{options})  bind/catch:increment="increment"
事件传递过来的数据放在event.detail中
父直接操作子 通过 const cpn=this.selectComponent(selector) 
可以直接操控cpn.setData  but not commend  commend call method
cpn.customethods  在cpn.__protop__中
seems no slot default value
use multiple slot should config Component({options:{"multipleSlots":true}})
Component({properties:{title:{type:String,value:"default",observer(nv,ov)=>{}}}
data:{},methods:{},options:{"multipleSlots":true,"styleIsolation"},externalClasses:[],observers:{couter:(newValue)=>{}}})
组件的生命周期,组件可以监听页面的生命周期,还有组件的生命周期,
pageLifetimes:{show(){},hide(){},resize(){"sizechange"}} 逐渐监听page生命周期
lifetimes:{created(){},attached(){'组件添加到页面'},ready(){'组件渲染完成'},moved(){'组件移动'},detached(){'组件移除'}}

Api
发送请求需要将url配置到控制台,不然不能发送,或者在设置里设置不校验
const _this=thiswx.request({url: 'http://123.207.32.32:8000/recommend',success(res){_this.setData({obj:res})} })  success==complete
注意this的指向  在调试器的 AppData中查找
wx.request({url:"",data:{type:"",page:""},header,method,dataType'返回数据的格式,JSON/??',success,,faile:err=>{},complete}) 成功失败完成
url:"http://httpbin.org/post" method:post  data:{random 随机写}
success:resolve  当成功时调用一个回调函数,并且把结果传递进这个函数

Toast
wx.showToast({title: '',})
wx.showModal({title:"",content:"",showCancel:"",success:res=>{console.log(res);}}) res.cancel  wx.showLoading()  wx.hideLoading() 显示和隐藏loading
wx.showActionSheet({itemList:[]}) 底部popup

weChat Share
onShareAppMessage(options){return{title:"hello weChat",path:"/pages/profile/profile",imageUrl:"默认将页面截图"}}
<button open-type="share">Share</button> 吃onShareAPPM的配置

weChat Login  (Miniprogram(小程序)、developerService(开发者服务器)、wechathttpapi(微信接口服务))
openID: weChat user unique identification 
session_key : pull with openId  本次登录的会话密钥
1.mini program call wx.login()  get code
2.mp wx.request()->ds  发送code  +小程序账户密码
3 ds  use  code+appid+appsecret(小程序密匙) ->登陆凭证校验接口 whp
4 whp 返回 session_key +openid
5自定义登陆状态,把openid 和程序自带的登陆注册关联
6ds 返回token 到mp 返回登陆状态 save in storage 无须每次都进行登陆操作 有时间期限token
7 mp -> wx.request() 携带token 发起请求  
8.dp 验证token (openid,session_key),success 返回数据
一、onLaunch wx.login({success:res=>{console.log(res.code);}})  code 只有5分钟liver
二、获取token  this.globalData.token = token wx.setStorageSync('token', token) 保存
三、 const token = wx.getStorageSync("token") 进来前判断token

页面跳转  navigator
<navigator url="/pages/detail/detail">Detail</navigator> 
<navigator open-type="navigateBack" delta="">back</navigator>  delta回退层数
open-type  switchTab 跳转到tabbar,并关闭所有非tabbar页面
redirect 跳转到一个非tabbar页面,并且不能返回
relaunch 关闭所有的页面,打开一个页面
页面跳转携带参数
url:"拼接" 在page({onLoad(options){console.log(options);}})
在onUnload(){const pages = getCurrentPages()获取栈的所有pages
const page = pages[pages.length-2] 获取上一个页面,page.setData....}
API 跳转  wx.navigator({url="/pages/detail/detail"})
wx.navigatorBack({delta:2})

Issue
在page直接修改component class会有 unexpected err
因为在微信小程序中组件是在#shadow-root之下的 所有组件实例的class  不等于 组件的class
data-index="{{index}}" 传递数据  在event.currentTarget.dataset.index get
triggerEvent()
函数下划线开头,私有函数_getData
Js对象添加键值对时,key要加中括号  字符串作为key可以不加 ''
 const pageKey = `goods.${type}.page` 中括号只能放变量或者数值
在WXSS中不能引入本地图片
hidden 属性对自定义组件无效,可以通过套一个view生效
官方建议不要再onPageScroll 中操作this.setData  frequently 太高
获取offset
wx.createSelectorQuery().select("selector").boundingClientRect(rect=>{console.log(rect)}).exec()
    wx.createSelectorQuery().select('#tabControl').boundingClientRect(function(rect){
        console.log(rect);
}).exec()
经测试,rect.top和移动的scrolltop有关,加上

<web-view src="https://www.baidu.com"></web-view>
跳转到out,out对应外部页面
get方法传递特殊符号字符串时
先将转换为json形式,再加码
const linkJson =JSON.stringify(link)  url: '/pages/out/out?url='+encodeURIComponent(linkJson),
parse  const url  =JSON.parse(decodeURIComponent(c.url))

scroll view 回到顶部 操控 attr scroll-top 
微信小程序部分shadow root  样式不生效,多尝试,
可通过传递样式

watch  computed
npm install --save miniprogram-computed
const computedBehavior = require('miniprogram-computed')
behaviors: [computedBehavior],
 sum(data) {// 注意： computed 函数中不能访问 this ，只有 data 对象可供访问// 这个函数的返回值会被设置到 this.data.sum 字段中return data.a + data.b},
watch:{num1(){this.setData({num2:200})}}
监听num1的改变去改变动态改变num2

