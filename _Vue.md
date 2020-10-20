# 	Vue

[toc]



## 基础

### 安装

兼容性    不支持ie8,兼容所有ECMA5

语义化版本控制    https://semver.org/lang/zh-CN/

Vue Devtools   https://github.com/vuejs/vue-devtools#vue-devtools

直接用\<script> 引入,Vue 会被注册成为一个全局变量    开发版本,生产版本(包含常见错误警告,大小) cdn,npm,yarn

对不同构件版本的解释   默认优先使vue.runtime.esm.js ES Moudle

需要编译器template,runtime-> render函数

```
module.exports = { // 配置使用其他版本
  resolve: {
    alias: {
      'vue$': 'vue/dist/vue.esm.js' // 用 webpack 1 时需用 'vue/dist/vue.common.js'}}}
```

配置开发环境和生产环境:保留process.env.NODE_ENV  在webpack 4 + 中 module.exports = {  mode: 'production' } 则 NODE_ENV=production低版本采用  [DefinePlugin](https://webpack.js.org/plugins/define-plugin/)：



### 介绍

声明式渲染 组件化应用构件,原始JS,命令式

### Vue实例

const vm = new Vue({  // 选项 })  viewmodel   所有的 Vue 组件都是 Vue 实例

Object.freeze() 冻结一个对象,包括原型也不可修改	

生命周期钩子   cretaed() 等 都是Vue的 static 方法

注意回调函数 与箭头函数的冲突

生命周期

### 模板语法

随意渲染html会有风险,容易导致XSS攻击,

模板表达式在沙盒内运行,只能访问全局变量的白名单,如Math,Date,不应在此访问自定义global variable

每个绑定{{}}只能包含一个表达式  表达式不能使用空格或引号,或用计算属性替代这种复杂表达式

v-bind:[attributeName]="url"  attributeName :'href  url:'.....'  属性名可用中括号绑定

html 属性名会被强制转换为小写

### 计算属性和侦听器

计算属性比方法多了一层缓冲

计算属性setter 比如属性之间有依赖关系,设置某个属性时,同时设置依赖属性

```
  watch: {
    $route: {
      handler: 'getDate',
      immediate: true
    }
  },
  // 监听路由,当组件复用时,也会去调用getDate函数,设置了immediate会在一开始进入时触发一次
  // deep 深度监听 为了发现对象内部值的变化
```



### Class与Style绑定

:class =  对象或数组

对象用于切换 ,可与普通的共存 ,也可bind数组,旨在于绑定变量的属性名,数组语法中也可以使用对象语法,

三元表达式绑定  ? : :

在组件上使用class会被添加到根元素上 ,shadow root则会出现与预期不同的结果

:style  内联绑定需为对象,绑定数组,数组中也要为对象.同理旨在于改变变量的属性名,useless

样式可以为kebab-case和camelCase kebab要加''

当:style 遇到需加厂商前缀的会自动添加

 :style="{ display: ['-webkit-box', '-ms-flexbox', 'flex'] }" 会渲染数组中最后一个被浏览器支持的值

### 条件渲染

v-show  不支持template ,即.vue文件根只能使用v-if

不推荐v-if 和 v-for同时使用  v-for具有更高的优先级,导致先遍历在判断v-if,可将v-if 置于外层

### 列表渲染

v-for  item in/of items

v-for = (value,index) in arr

v-for= (value,key,index) in obj   遍历对象采用的是原生Object.key value()方法

当vue热更新v-for渲染的元素时,采用就地更新策略,当顺序改变时,将不会移动Dom元素,这种策略在应对插入中间元素时略显笨拙,可使用key解决

key 只能为string/number    can't be arr/obj

push() pop() shift() unshift() splice() sort() reverse() 会触发热更新,因为改变了原数组

filter() concat() slice() 相对的临时改变不会触发

在组件上使用v-for 时, key时必须的

is 属性 因为在dom模板中 例如ul中只有li会被看作有效内容,若想在ul中使用组件,必须使用ul>[is = 组件名]li,因此绑定is :is=''可用于切换子组件

### 事件处理

当了绑定方法可传参数,默认传 $event  ,也可在携带参数同时,主动传

修饰符 .stop  阻止传播 .prevent  提交不重载页面 .capture捕获模式,即冒泡触发时事件顺序.self 只有触发元素为自身才触发  .once 只触发一次

可串联 v-on:click.prevent.self会阻止所有的点击，而 v-on:click.self.prevent`只会阻止对元素自身的点击。

.passive 等待时间如scroll停止才触发

input 框 v-on:keyup.enter 当回车时才触发  查阅keyboardevent.key

按键码 keycode 已被废弃,最好采用board alias

可全局Vue.config.keyCodes.f1 = 112配置keycode别名

.ctrl  .alt .shift .meta 同时按下才触发 ,例如ctrl加单击

.exact  click.ctrl 会被 ctrl 和ctrl➕alt 触发  click.ctrl.exact只会被ctrl触发

.left  .right .middle 修饰鼠标

### 表单输入绑定

v-model 会忽略表单绑定的属性initial value ,而选择data中的初始值

text,textarea绑定  value属性和input事件

checkbox绑定 checked 和change事件

select绑定value和change事件

select 中的选项options 如果没有绑定初始值的话,options中的文本将会作为初始值,但在ios中用户将不会选择第一个选项,因为无法触发change事件,可将第一个选项置为disable,value='' 的desc 占位

值绑定,当selected 开启v-model时,options 的值会替代整个v-model对应的变量, 但变量可以是一个对象,options v-bind:vlaue={foo:123} 绑定变量中的foo属性

v-model  .lazy 输入完时才绑定 .number 转换为数字类型

### 组件基础

data必须是一个函数,为了独立维护他的data

每个组件必须只有一个根元素 

$emit(eventName,payload)

v-model 如果双向绑定的值在父组件,input在子组件时,相当于\<cpn :value='' @input='count=$event'>,绑定value,监听input事件

\<component>中有一个is属性 值可以为组件名,或者组件对象 同理is 可用于html严格限制某些元素内部使用组件入ul>[is='cpn']li 

html这种限制在模板内容都是字符串,单文件组织,\<script type='text/x-template'> 不生效

## 深入了解组件

### 组件注册

注册时 Pascal case 使用时 kebab lower case

基础组件的自动化全局注册

req.require.context(directory, useSubdirectories, regExp) 路径,是否查找子目录,正则表达式

返回一个函数 webpackContext

所以req.keys() = map.key 组成的数组 map是模块内部变量，无法直接访问，所以通过其实提供的keys方法访问

```
const importAll =r=>r.keys().forEach(r)
const requireAll = requireContext => requireContext.keys().map(requireContext)

importAll(require.context('./components/', true, /\.js$/))
```

执行require.context返回的函数

### Prop

在非字符串模板 props 没有kebab-case,变量不能有- ,camelCase,PascalCase需使用kebab-case 

组件名,注册和使用同理

在字符串模板没有这些限制,即.vue文件

传数字,默认传的都是string,静态传number 需v-bind

传布尔值,模板传true可直接写布尔属性(必须声明为Boolean类型) ,传false需v-bind,非模板都需要手动绑定 true,false

如果你想将一个对象所有的property 都作为prop传入,可以使用不带参数的v-bind= 'obj',v-bind一个对象相当于将对象所有的key还有值静态传入,如果key为class即为样式

不应在子组件内部改变prop,console会发出警告,应用一另外的变量来先接收,或计算属性操作

在子组件改变父组件传来的obj,arr会影响父组件,因为对象传递的是深拷贝的引用

Prop验证,无验证-> props:[propa]                                                                                                                                   验证 props : { propa:Number, propb:[Number,String] 多类型,propc:{require:ture,必传值,default:100 默认值}} 

default:function(){return {}}默认对象值,需为工厂函数 

指定值 propF: {      validator: function (value) { return ['success', 'warning', 'danger'].indexOf(value) !== -1  }   }

type : String,Number,Boolean,Array,Object,Date,Function,Symbol ,还可以是一个自定义的构造函数,验证prop是否为函数的实例

如果你不希望组件的根元素继承 attribute，你可以在组件的选项中设置 `inheritAttrs: false`。如果子组件的根元素就是一个input ,此时在子组件绑定value会直接继承到子组件上,并不需要通过props

$attrs 包含了父作用域中不作为 prop 被识别 (且获取) 的 attribute 绑定 (`class` 和 `style` 除外)。vite中渲染结果包含class

### 自定义事件

我们推荐你**始终使用 kebab-case 的事件名**

自定义组件v-model,默认传了一个props为value,(仍要写props)监听事件为input.会绑定组件内所有元素的,可通过model: { prop: 'checked',  event: 'change'  }避免冲突<input type="text" :value="checked" @input="$emit('change',$event.target.value)" />,在vite结果不相同

.native  自定义事件不需要,比如子组件根元素发出的自定义事件,原生事件,如子组件点击需要.native监听

但有些情况.native监听不到,比如输入框的onfocus事件,如果输入框就是根组件,那么.natvie可以正常监听,如果不是则,$listeners要上场了.它是一个事件对象.包含了父作用域中的 (不含 `.native` 修饰器的) `v-on` 事件监听器。它可以通过 `v-on="$listeners"` 传入内部组件——在创建更高层次的组件时非常有用。(父组件监听focus事件,子组件通过$listeners得到父组件监听的事件,v-on监听这个事件)

v-on:click = 'fn' 监听click事件,触发fn函数  v-on="{click:function(){}}"  监听事件对象,事件对象中有click事件

v-on和 v-on:input 等不共存,v-on='计算属性' return Object.assign(target,source1,source2)

通常使用 update:变量名   子组件更新父组件值时,采用this.$emit('update:title', newValue) @update:propName='propName=$event',方式此时自定义事件中的$event即为传过来的值

可使用:value.sync='value' 来简写去掉 @update:prop,但组件内部emit 事件名需配套写层update:propName

也可以通过v-bind.sync="obj" 批量缩写,记得`v-bind.sync=”{ title: doc.title }”`，是无法正常工作的,这样会把 `doc` 对象中的每一个 property (如 `title`) 都作为一个独立的 prop 传进去，然后各自添加用于更新的 `v-on` 监听器。

### 插槽

模板中\<slot name='c'>\</slot>会被替换  \<div slot='c'/>(旧用法)  \<template v-slot:c>

父级模板里的所有内容都是在父级作用域中编译的；子模板里的所有内容都是在子作用域中编译的。

作用域插槽,即插槽内容想访问模板中的数据. 模板中 \<slot :data='data'  或者 v-bind='obj'>                                                                     使用时\<template v-slot='cdata'>{{cdata.data}}\</template>

v-slot默认只能写在template上,有一种情况例外,如果模板中只有一个默认插槽,那么插槽连v-slot都不用写.但此时默认插槽又用到了作用域插槽,就可以直接在自定义组件上v-slot='变量名'

作用域插槽和具名插槽可以混用,例如v-slot:center='cdata',但只能在template,而不能在自定义组件,因为自定义组件只能插入默认插槽

解构插槽,作用域插槽时,子组件绑定的数据工作原理是将你的插槽内容包括在一个传入单个参数的函数里然后返回一个对象,如果子组件:obj=obj 父组件 v-slot{obj:{key1,key2}},如果v-bind='obj' v-slot='{key1,key2}'

动态插槽名,即插槽名可以用一个计算属性计算  v-slot:center  vl-slot:[getSlotName]

具名插槽的缩写 v-slot:center  -> #center  template中 #center='ATTRNAME'  #:default='ATTRNAME' 还不如写v-slot='attrname'

 废弃了的语法 slot,将不会出现在Vue3.0  可绑定在任意元素上, \<h1 slot='center'> 

**默认插槽**具名插槽外的所有内容会被置于空 \<slot>中,当然前提是要有

废弃了的作用域插槽\<slot-scope>='变量名' 同样可绑定在任意元素上,但写template是官方推荐的写法

### 动态组件&异步组件

切换路由切换大组件,is切换小组件 \<keep-alive> 保护不被销毁 ,保护的子组件必须有name这个选项

异步组件,通常用于路由切换,只在需要用到的时候才加载,并且会把结果缓存起来

单页面异步:

```
Vue.component('async-example', function (resolve, reject) {// 传入resolve,reject
  setTimeout(function () {
    // 向 `resolve` 回调传递组件定义
    resolve({
      template: '<div>I am async!</div>'
    })
  }, 1000)
}) 例如导入成功调..失败调....
```

webpack中的code-splitting

```
  components: {
    cpn: function (resolve) {
      // 这个特殊的 `require` 语法将会告诉 webpack
      // 自动将你的构建代码切割成多个包，这些包
      // 会通过 Ajax 请求加载
      require(['./Child'], resolve)
    }
  },
```

结合webpack和es2015

```
  components: {cpn: ()=>import("./Child")},
```

处理加载状态

```
  const AsyncComponent=() => ({   // 用箭头函数返回对象加()表示内容为返回,防止{}不明义
      // 需要加载的组件 (应该是一个 `Promise` 对象)
      component: import('./Child'),
      // 异步组件加载时使用的组件
      // loading: LoadingComponent,
      // // 加载失败时使用的组件
      // error: ErrorComponent,
      // 展示加载时组件的延时时间。默认值是 200 (毫秒)
      delay: 200,
      // 如果提供了超时时间且组件加载也超时了，
      // 则使用加载失败时使用的组件。默认值是：`Infinity`
      timeout: 3000
    })
  components: {
    cpn: AsyncComponent
  },
```

注意如果你希望在 [Vue Router](https://github.com/vuejs/vue-router) 的路由组件中使用上述语法的话，你必须使用 Vue Router 2.4.0+ 版本。

### 处理边界情况

危险的慎用,访问根实例,$root,小型项目可用于管理状态,当然大型项目还是推荐Vuex

$parent访问父组件实例

访问子组件,使用属性ref引用,推荐 ref=clc  this.$refs.clc  但要避免在模板或计算属性中访问 `$refs`,因为他不是响应式的,只会在组件渲染 完成之后生效

provide和inject 在祖代provide,后代都可以inject

```
provide: function () {
  return {
    getMap: this.getMap
  }
}
inject: ['getMap']  调用 直接this.getMap()
```

相比$parent优点在于不用担心中间隔代,子组件访问无须关心函数来源于哪,当然依旧耦合,当程序多的时候,VueX

程序化的事件监听器

- 通过 `$on(eventName, eventHandler)` 侦听一个事件
- 通过 `$once(eventName, eventHandler)` 一次性侦听一个事件
- 通过 `$off(eventName, eventHandler)` 停止侦听一个事件

以前创建一个引入库的实例,eg this.scroll  在beforeDestroy: function () {  this.scroll  .destroy()  这种做法需要在实例this中保存这个变量,可通过创建时,手动监听销毁事件  this.$once('hook:beforeDestroy', function () {} console.log('我被销毁了')}) 事件名 hook:beforeDestory、

当name和template有相同组件时,即递归组件会报Maximum call stack size exceeded error

组件之间的循环调用,父中有子,子中有父,但是是有条件的悖论时,如果是全局注册的,没事,如果是模块系统导入的,例如webpack就会报错因为webpack导入会导致循环依赖的问题,解决办法,产生悖论的时子组件.子组件不采用直接导入的方式,而是

```
导入子组件时采用
beforeCreate: function () {
  this.$options.components.TreeFolderContents = require('./tree-folder-contents.vue').default
}
// 或者在注册时异步导入
components: {
  TreeFolderContents: () => import('./tree-folder-contents.vue')
}
就不会有递归依赖的问题
```

内敛模板 一个组件即使没有插槽,也可以通过属性inline-template 强制更换模板

X-Template 单页面应用中 \<script type='text/x-template' id='app'> \<template id=''>  注册时template:'#app'

控制更新,当你觉得你需要强制更新的时候,那么99.99情况是因为你其他代码错了,如果不是可采用$forceUpate

通过v-once \<div v-once / > 当这个组件包含大量的文本,可采用此方法使其只计算一次并且存储起来,当然会导致整个子组件失去热更新,慎用

## 过渡&动画

### 进入/离开 & 列表过渡 

CSS过渡 \<transition name='fade'> 包裹 

```
// 样式可设置为全局
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
```

当插入或者删除transition中的元素时(监测v-show,v-if ),Vue会进行以下处理,自动嗅探是否应用了CSS过渡或者动画,在恰当是时机添加/删除CSS类名,如果添加了JavaScript函数,会在恰当的时机调用,如果都没有,会在Dom下一帧中立即执行

在进入/离开的过渡中，会有 6 个 class 切换。

1. `v-enter`：定义进入过渡的开始状态。在元素被插入之前生效，在元素被插入之后的下一帧移除。
2. `v-enter-active`：定义进入过渡生效时的状态。在整个进入过渡的阶段中应用，在元素被插入之前生效，在过渡/动画完成之后移除。这个类可以被用来定义进入过渡的过程时间，延迟和曲线函数。
3. `v-enter-to`：在元素被插入之后下一帧生效 (与此同时 `v-enter` 被移除)，在过渡/动画完成之后移除。
4. `v-leave`：定义离开过渡的开始状态。在离开过渡被触发时立刻生效，下一帧被移除。
5. `v-leave-active`：定义离开过渡生效时的状态。在整个离开过渡的阶段中应用，在离开过渡被触发时立刻生效，在过渡/动画完成之后移除。这个类可以被用来定义离开过渡的过程时间，延迟和曲线函数。
6. `v-leave-to`：在离开过渡被触发之后下一帧生效 (与此同时 `v-leave` 被删除)，在过渡/动画完成之后移除。

如果transition没有name属性,则类名即为上面这些类名,若为name='fade'则类名对应改变为faed-enter,fade-enter-active......

CSS 动画用法同 CSS 过渡,却别在于v-enter是在插入dom下一帧移除,而动画是在`animationend` 事件触发时删除

```
.bounce-enter-active {
  animation: bounce-in .5s;
}.bounce-leave-active {
  animation: bounce-in .5s reverse; //reverse 直接反转
}@keyframes bounce-in {
  0% {transform: scale(0);}
  50% {transform: scale(1.5);}
  100% {transform: scale(1);}}
```

自定义过渡类名,比如css样式库已经写好的无法改变的样式名,可通过transition上的这些属性绑定

- `enter-class`
- `enter-active-class`
- `enter-to-class` (2.1.8+)
- `leave-class`
- `leave-active-class`
- `leave-to-class` (2.1.8+)

Vue为了知道过渡或者动画的完成,会给事件设置对应的事件监听器.transitioned或animationed,如果设置动画或者过渡,Vue会自动识别并设置监听,但如果同时有过渡和动画.比如 `animation` 很快的被触发并完成了，而 `transition` 效果还没结束。在这种情况中，你就需要使用 `type` attribute 并设置 `animation` 或 `transition` 来明确声明你需要 Vue 监听的类型。

在很多情况下，Vue 可以自动得出过渡效果的完成时机。比如说当动画结束时过渡完成.可通过\<transition>上的组件 prop :duration="1000"  :duration="{ enter: 500, leave: 800 }" 定义过渡完成的时机

JavaScript钩子

可以在 attribute 中声明 JavaScript 钩子

```
<transition
  v-on:before-enter="beforeEnter"
  v-on:enter="enter"
  v-on:after-enter="afterEnter"
  v-on:enter-cancelled="enterCancelled"

  v-on:before-leave="beforeLeave"
  v-on:leave="leave"
  v-on:after-leave="afterLeave"
  v-on:leave-cancelled="leaveCancelled"
>
  <!-- ... -->
</transition>
```

enter和leave有两个参数(el,done) 其余只有el  done()被调用的话,动画或者过渡立即完成,当使用js进行过渡时,必须使用done回调.推荐对于仅使用 JavaScript 过渡的元素添加 `v-bind:css="false"`，Vue 会跳过 CSS 的检测。这也可以避免过渡过程中 CSS 的影响。只是用js过渡.

初始渲染的过渡,也就是第一次进来的动画/过渡

通过appear属性 ,appear 和上面的JS钩子不共存,会导致appear失效

```
<transition
  appear
  appear-class="custom-appear-class"
  appear-to-class="custom-appear-to-class" (2.1.8+)
  appear-active-class="custom-appear-active-class"
>
  <!-- ... -->
</transition>
```

appear钩子

```
<transition
  appear
  v-on:before-appear="customBeforeAppearHook"
  v-on:appear="customAppearHook"
  v-on:after-appear="customAfterAppearHook"
  v-on:appear-cancelled="customAppearCancelledHook"
>
  <!-- ... -->
</transition>
```

多个元素过渡时,在使用v-if  v-else切换元素时有一点要注意,那就是当切换的元素时相同的元素,必须要设置key来区分,否则Vue会为了效率只替换内容,

多个元素过渡默认行为是同时进行的,会导致div有种顿挫感,可以设置绝对定位在同一个位置.或者设置\<transition>的mode= ""  `in-out`：新元素先进行过渡，完成之后当前元素过渡离开 `out-in`：当前元素先进行过渡，完成之后新元素过渡进入。通常都是用out-in,leave-> enter

多个组件切换过渡只需要用 动态组件is切换即可,样式等同会自动添加

列表过渡 需要用到\<transition-group>元素,不同于\<transition>不渲染 他会以一个真实元素 默认\<span>呈现,可通过tag切换为其他.

列表过渡中的元素不能再进行多个元素/组件过渡,并且需要为一个key值.CSS 过渡的类将会应用在内部的元素中，而不是这个组/容器本身。

如此初步列表渲染以完成,但有一个小问题,新插入的元素影响已有元素位置的改变是瞬间变化的,所以可以用\<transition-group>特有的v-move class 同样的他会被name 改变前缀 也可以通过move-class手动自定义设置,

```
.v-move{transition:transform:1s}
也可以直接写在遍历的元素上 <span v-for class='???'>
.???{transition:all 1s}写在这个位置,等于v-mode和 leave/enter active
并且.v-move对删除元素还需设置.vleave-active { position: absolute;} 才生效
```

这个看起来很神奇，内部的实现，Vue 使用了一个叫 FLIP 简单的动画队列
使用 transforms 将元素从之前的位置平滑过渡新的位置。
需要注意的是使用 FLIP 过渡的元素不能设置为 display: inline 。作为替代方案，可以设置为 display: inline-block 或者放置于 flex 中

列表过渡中如果希望批量添加删除元素动画添加间隔,目前只有js才能办得到,css不行

过渡可以通过 Vue 的组件系统实现复用。要创建一个可复用过渡组件，你需要做的就是将 `<transition>` 或者 `<transition-group>` 作为根组件，然后将任何子组件放置在其中就可以了。

动态过渡:基本用法比如绑定transition上的name ,然后根据name对应不同的样式,

循环,过渡和动画都是因为插入或者删除改变的,只要在插入时删除,删除时插入即可实现循环.例如呼吸灯

### 状态过渡

进入离开过渡必须触发进入离开,状态过渡即数据元素本身动效

通过watch监听数字变化,触发动画

## 可复用性&组合

### 混入

var Component = Vue.extend({  mixins: [myMixin] })  var component = new Component()  extend创建出来的组件构造器可以进行注册,也可以直接new 一个实例

选项合并,当组件和mixindata有同名时,会以组件的优先.相同的钩子函数,生命周期函数会合并成一个数组,并且mixin先调用.值为对象的选项.比如methods,components,directives会被合并为一个对象,以cpn优先

全局混入.即执行 Vue.mixin() 可以用来为自定义选项注入处理逻辑

```
Vue.mixin({created(){console.log('我是全局混入');}})
```

```
Vue.mixin({
  created() {
    if (this.$options.customOption) {
      console.log(this.$options.customOption);
    }
  }
}) // 自定义选项,即Vue下的所有选项都会存在$options中大多数情况下，全混只应当应用于自定义选项
```

自定义选项将使用默认策略，即简单地覆盖已有值。(组件覆盖混入)如果想让自定义选项以自定义逻辑合并，可以向 `Vue.config.optionMergeStrategies` 添加一个函数：

```
Vue.config.optionMergeStrategies.customOptions = function(toVal, fromVal) {
  if (!toVal) return fromVal
  return fromVal >= toVal ? fromVal : toVal
}
执行两次,// toVal第一次undefined 第二次为第一次返回值 fromVal 第一次为mixin的值 第二次为组件中的值
```

对于多数值为对象的选项，可以使用与 `methods` 相同的合并策略：即默认情况是整个对象都被cpn的对象替换,而不是像methods设计好的相同合并,盈余兼容.

```
var strategies = Vue.config.optionMergeStrategies
strategies.myOption = strategies.methods
```

可以在 [Vuex](https://github.com/vuejs/vuex) 1.x 的混入策略里找到一个更高级的例子：

```
const merge = Vue.config.optionMergeStrategies.computed
Vue.config.optionMergeStrategies.vuex = function (toVal, fromVal) {
  if (!toVal) return fromVal
  if (!fromVal) return toVal
  return {
    getters: merge(toVal.getters, fromVal.getters),
    state: merge(toVal.state, fromVal.state),
    actions: merge(toVal.actions, fromVal.actions)
  }
}
```

### 自定义指令

全局自定义指令v-focus

```
// focus.js
const install = Vue => {
  Vue.directive('focus', {
    inserted: function(el) {
      el.focus()
    }
  })
}
module.exports = install
// index.js
import Vue from 'vue'
const req = require.context('./', false, /[^index]\.js$/)
const requireAll = requireContext => requireContext.keys().map(_ => Vue.use(requireContext(_)))
requireAll(req)
// main.js
import './directive'
```

也能局部注册

```
directives: {
  focus: {
    // 指令的定义
    inserted: function (el) {
      el.focus()
    }
  }
}
```

一个自定义指令可以提供如下几个钩子函数 (均为可选)：

- `bind`：只调用一次，指令第一次绑定到元素时调用。在这里可以进行一次性的初始化设置。
- `inserted`：被绑定元素插入父节点时调用 (仅保证父节点存在，但不一定已被插入文档中)。
- `update`：所在组件的 VNode 更新时调用，**但是可能发生在其子 VNode 更新之前**。指令的值可能发生了改变，也可能没有。但是你可以通过比较更新前后的值来忽略不必要的模板更新 (详细的钩子函数参数见下)。
- `componentUpdated`：指令所在组件的 VNode **及其子 VNode** 全部更新后调用。
- `unbind`：只调用一次，指令与元素解绑时调用。

接下来我们来看一下钩子函数的参数 (即 `el`、`binding`、`vnode` 和 `oldVnode`)。

- `el`：指令所绑定的元素，可以用来直接操作 DOM。

- ```
  binding
  ```

  ：一个对象，包含以下 property：

  - `name`：指令名，不包括 `v-` 前缀。
  - `value`：指令的绑定值，例如：`v-my-directive="1 + 1"` 中，绑定值为 `2`。
  - `oldValue`：指令绑定的前一个值，仅在 `update` 和 `componentUpdated` 钩子中可用。无论值是否改变都可用。
  - `expression`：字符串形式的指令表达式。例如 `v-my-directive="1 + 1"` 中，表达式为 `"1 + 1"`。
  - `arg`：传给指令的参数，可选。例如 `v-my-directive:foo` 中，参数为 `"foo"`。
  - `modifiers`：一个包含修饰符的对象。例如：`v-my-directive.foo.bar` 中，修饰符对象为 `{ foo: true, bar: true }`。

- `vnode`：Vue 编译生成的虚拟节点。移步 [VNode API](https://cn.vuejs.org/v2/api/#VNode-接口) 来了解更多详情。virtual node 虚拟节点

- `oldVnode`：上一个虚拟节点，仅在 `update` 和 `componentUpdated` 钩子中可用。

  除了 `el` 之外，其它参数都应该是只读的，切勿进行修改。如果需要在钩子之间共享数据，建议通过元素的 [`dataset`](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLElement/dataset) 来进行。

  动态指令参数   v-mydirective:argument="value"  binding.arg = argument    v-mydirective:[argument]="value"   argument='foo' bingding.arg = foo

函数简写

在很多时候，你可能想在 `bind` 和 `update` 时触发相同行为，而不关心其它的钩子。比如这样写：

```
Vue.directive('color-swatch', function (el, binding) {
  el.style.backgroundColor = binding.value
})// 绑定时执行一次,更新也会执行
```

自定义指令 v-focus可以绑定一个对象,那么value就是这个对象

### 渲染函数&JSX

Vue在绝大多数情况下推荐你使用模板单文件语法.但有的时候你可以用渲染函数,不需要模板编译器.

vue template proces 保存在 options 中 ->解析成 ast(抽象语法树)abstract syntax tree
->编译vue options 中的 render 函数 -> 渲染virtual dom-> ui

比如在模板中有大量的重复的有关联的逻辑代码时.此时可以使用render函数,首先要弄懂这个createElement函数

```
cpn: {
      render: function (h) {
        console.log(h); // -> createElement(tag,attr,VNode)
        console.log(this); 组件实例
        console.log(this.level); 组件实例pros属性,必须在下方声明
        console.log(this.$slots.default);
        // this.$slots是一个对象,里面有一个key为default的 VNODE数组
        // cpn插槽的内容在VNODE0号元素的text上
        console.log(h('h1',this.$slots.default));
        return h(Child)// 可以直接传一个单文件,
      },
      props: { // 和render函数同级的, <cpn :level='1'> render函数红this.level才能拿得到
        level: {
          type: Number,
          required: true
        }
      }
    }
```

向组件中传递不带 `v-slot` 指令的子节点时，比如 cpn 中的 `Hello world!`，这些子节点被存储在组件实例中的 `$slots.default` VNODE0号元素的text上

`createElement` 到底会返回什么呢？其实不是一个*实际的* DOM 元素。它更准确的名字可能是 `createNodeDescription`，因为它所包含的信息会告诉 Vue 页面上需要渲染什么样的节点，包括及其子节点的描述信息。我们把这样的节点描述为“虚拟节点 (virtual node)”，也常简写它为“**VNode**”。“虚拟 DOM”是我们对由 Vue 组件树建立起来的整个 VNode 树的称呼。

createElement() 参数  

1.   // {String | Object | Function}  // 一个 HTML 标签名、组件选项对象，或者  // resolve 了上述任何一种的一个 async 函数。必填项。  'div',  或者main.js 函数中的 App
2. {Object}  可选,attr对象
3. {String|Array}  h()或者字符串

深入数据对象,即 h函数的第二个参数 attr对象

```
{
  // 与 `v-bind:class` 的 API 相同，
  // 接受一个字符串、对象或字符串和对象组成的数组
  'class': {
    foo: true,
    bar: false
  },
  // 与 `v-bind:style` 的 API 相同，
  // 接受一个字符串、对象，或对象组成的数组
  style: {
    color: 'red',
    fontSize: '14px'
  },
  // 普通的 HTML attribute
  attrs: {
    id: 'foo'
  },
  // 组件 prop
  props: {
    myProp: 'bar'
  },
  // DOM property
  domProps: {
    innerHTML: 'baz'
  },
  // 事件监听器在 `on` 内，
  // 但不再支持如 `v-on:keyup.enter` 这样的修饰器。
  // 需要在处理函数中手动检查 keyCode。
  on: {
    click: this.clickHandler
  },
  // 仅用于组件，用于监听原生事件，而不是组件内部使用
  // `vm.$emit` 触发的事件。
  nativeOn: {
    click: this.nativeClickHandler
  },
  // 自定义指令。注意，你无法对 `binding` 中的 `oldValue`
  // 赋值，因为 Vue 已经自动为你进行了同步。
  directives: [
    {
      name: 'my-custom-directive',
      value: '2',
      expression: '1 + 1',
      arg: 'foo',
      modifiers: {
        bar: true
      }
    }
  ],
  // 作用域插槽的格式为
  // { name: props => VNode | Array<VNode> }
  scopedSlots: {
    default: props => createElement('span', props.text)
  },
  // 如果组件是其它组件的子组件，需为插槽指定名称
  slot: 'name-of-slot',
  // 其它特殊顶层 property
  key: 'myKey',
  ref: 'myRef',
  // 如果你在渲染函数中给多个元素都应用了相同的 ref 名，
  // 那么 `$refs.myRef` 会变成一个数组。
  refInFor: true
}
      methods: {
        clickHandler() {
          console.log(123);
        },
        onClick() {
          console.log(456);
        }
      },
      data(){
      reutrn{count:123}
      }
    } // 方法都写在render同级下的method 
```

 // 组件 prop  props: {    myProp: 'bar'  }, 绑定给下一个节点为组件的prop

 // nativeOn: {    click: this.nativeClickHandler  },监听下一个节点 $emit出来的事件

约束组件树中的所有 VNode 必须是唯一的。这意味着，下面的渲染函数是不合法的：

```
render: function (createElement) {
  var myParagraphVNode = createElement('p', 'hi')
  return createElement('div', [
    // 错误 - 重复的 VNode
    myParagraphVNode, myParagraphVNode
  ])
} // 实际测试时合法的
```

```
render: function (createElement) {
  return createElement('div',
    Array.apply(null, { length: 20 }).map(function () {
      return createElement('p', 'hi')
    })
  )
}// 如果你真的需要重复很多次的元素/组件，你可以使用工厂函数来实现
```

render函数中的v-if和v-for

```
props: ['items'],
render: function (createElement) {
  if (this.items.length) {
    return createElement('ul', this.items.map(function (item) {
      return createElement('li', item.name)
    }))
  } else {
    return createElement('p', 'No items found.')
  }
}
```

渲染函数中没有与 `v-model` 的直接对应——你必须自己实现相应的逻辑：

```
      render(h) {
        return h('div', {
          props: {
            value: this.value
          },
        }, [h('input', {
          domProps: {
            value: this.value
          },
          on:{
            input:_=>{
              this.$emit('input',_.target.value)
            }
          }
        }),])
      },
      props: ['value']
    },
```

事件&按键修饰符:对于 `.passive`、`.capture` 和 `.once` 这些事件修饰符，Vue 提供了相应的前缀可以用于 `on`

| `.passive`                         | `&`  |
| ---------------------------------- | ---- |
| `.capture`                         | `!`  |
| `.once`                            | `~`  |
| `.capture.once` 或 `.once.capture` | `~!` |

```
on: {
  '!click': this.doThisInCapturingMode,
  '~keyup': this.doThisOnce,
  '~!mouseover': this.doThisOnceInCapturingMode
}
```

 this.$scopedSlots 访问作用域插槽，每个作用域插槽都是一个返回若干 VNode 的函数：

```
        return createElement('div', [
          this.$scopedSlots.default({
            text: 'hha'
          })])
```

JSX语法

```
import AnchoredHeading from './AnchoredHeading.vue'

new Vue({
  el: '#demo',
  render: function (h) {
    return (
      <AnchoredHeading level={1}>
        <span>Hello</span> world!
      </AnchoredHeading>
    )
  }
})
```

函数式组件:没有管理任何状态，也没有监听任何传递给它的状态，也没有生命周期方法。标记为 `functional`，这意味它无状态 (没有[响应式数据](https://cn.vuejs.org/v2/api/#选项-数据))，也没有实例 (没有 `this` 上下文)。一个**函数式组件**就像这样：

注意：在 2.3.0 之前的版本中，如果一个函数式组件想要接收 prop，则 `props` 选项是必须的。在 2.3.0 或以上的版本中，你可以省略 `props` 选项，所有组件上的 attribute 都会被自动隐式解析为 prop。

```
Vue.component('my-component', {
  functional: true,
  // Props 是可选的
  props: {
    // ...
  },
  // 为了弥补缺少的实例
  // 提供第二个参数作为上下文
  render: function (createElement, context) {
    // ... 多了context参数
    // console.log(this) // null 没有this
  }
})
```

单文件的函数式组件

```
<template functional>
</template>
```

组件需要的一切都是通过 `context` 参数传递，它是一个包括如下字段的对象：

- `props`：提供所有 prop 的对象
- `children`：VNode 子节点的数组
- `slots`：一个函数，返回了包含所有插槽的对象
- `scopedSlots`：(2.6.0+) 一个暴露传入的作用域插槽的对象。也以函数形式暴露普通插槽。
- `data`：传递给组件的整个[数据对象](https://cn.vuejs.org/v2/guide/render-function.html#深入数据对象)，作为 `createElement` 的第二个参数传入组件
- `parent`：对父组件的引用
- `listeners`：(2.3.0+) 一个包含了所有父组件为当前组件注册的事件监听器的对象。这是 `data.on` 的一个别名。
- `injections`：(2.3.0+) 如果使用了 [`inject`](https://cn.vuejs.org/v2/api/#provide-inject) 选项，则该对象包含了应当被注入的 property。

在添加 `functional: true` 之后，需要更新我们的锚点标题组件的渲染函数，为其增加 `context` 参数，并将 `this.$slots.default` 更新为 `context.children`，然后将 `this.level` 更新为 `context.props.level`。

因为函数式组件只是函数，所以渲染开销也低很多。

在作为包装组件时它们也同样非常有用。比如，当你需要做这些时：

- 程序化地在多个组件中选择一个来代为渲染；
- 在将 `children`、`props`、`data` 传递给子组件之前操作它们。

```
    cpn: {
      functional:true,
      render: function (h,context) {
        return h(`h${context.props.level}`,context.children)
      }
    },函数式组件形势的渲染函数
```

重点:因为函数式组件只是函数，所以渲染开销也低很多。

```
  render: function (createElement, context) {
    function appropriateListComponent () {
      var items = context.props.items

      if (items.length === 0)           return EmptyList
      if (typeof items[0] === 'object') return TableList
      if (context.props.isOrdered)      return OrderedList

      return UnorderedList
    }

    return createElement(
      appropriateListComponent(),
      context.data,
      context.children
    ) // 可用于切换组件
```

智能合并  context.data就是h函数第二个参数数据对象

单文件函数式组件

```
<cpn @click="onClick" name='button'></cpn>
<template functional>
  <button v-on='listeners'>{{data.attrs.name}}</button>
</template> 
// 不用加 $
```

### 插件

插件通常用来为 Vue 添加全局功能。插件的功能范围没有严格的限制——一般有下面几种：

plugins/index

1. 添加全局方法或者 property。如：[vue-custom-element](https://github.com/karol-f/vue-custom-element) 添加到类的静态上
2. 添加全局资源：指令/过滤器/过渡等。如 [vue-touch](https://github.com/vuejs/vue-touch), Toast 指令
3. 通过全局混入来添加一些组件选项。如 [vue-router](https://github.com/vuejs/vue-router),混入一下customOptions
4. 添加 Vue 实例方法，通过把它们添加到 `Vue.prototype` 上实现。添加到原型
5. 一个库，提供自己的 API，同时提供上面提到的一个或多个功能。如 [vue-router](https://github.com/vuejs/vue-router)

Vue.use 安装 Vue.js 插件。如果插件是一个对象，必须提供 `install` 方法。如果插件是一个函数，它会被作为 install 方法。install 方法调用时，会将 Vue 作为参数传入。也可以传入一个可选的选项对象：

```
Vue.use(MyPlugin, { someOption: true }) 安装vant比如
```

第二个参数options 在install执行时第二个参数传入

### 过滤器

|   过滤器可以用在两个地方：**双花括号插值和 `v-bind` 表达式**

```
  filters:{
    formatPrice(v){
      return v*10
    }
  }// 局部注册
  Vue.filter('capitalize', function (value) {
  if (!value) return ''
  value = value.toString()
  return value.charAt(0).toUpperCase() + value.slice(1)
})// 全局注册
```

```
因为注册大多比较小,放在一个文件夹下,就可以通过
export function的形势, 在对象中 ,函数名:函数
Object.keys(filters).forEach(key => {
  Vue.filter(key, filters[key])
})

```

当全局过滤器和局部过滤器重名时，会采用局部过滤器。

过滤器可以串联 {{ message | filterA | filterB }}

过滤器是 JavaScript 函数，因此可以接收参数：{{ message | filterA('arg1', arg2) }}

## 工具

### 单文件组织

看VueCLI把

### 测试

三大类:单元测试,组件测试,e2e端到端测试

单元测试允许你将独立单元的代码进行隔离测试，其目的是为开发者提供对代码的信心。

Jest 是一个专注于简易性的 JavaScript 测试框架。一个其独特的功能是可以为测试生成快照 (snapshot)，以提供另一种验证应用单元的方法。

Mocha 是一个专注于灵活性的 JavaScript 测试框架。因为其灵活性，它允许你选择不同的库来满足诸如侦听 (如 Sinon) 和断言 (如 Chai) 等其它常见的功能。另一个 Mocha 独特的功能是它不止可以在 Node.js 里运行测试，还可以在浏览器里运行测试。

组件测试测试大多数 Vue 组件时都必须将它们挂载到 DOM (虚拟或真实) 上，才能完全断言它们正在工作。这是另一个与框架无关的概念

Vue Testing Library 是一组专注于测试组件而不依赖实现细节的工具。由于在设计时就充分考虑了可访问性，它采用的方案也使重构变得轻而易举。

Vue Test Utils 是官方的偏底层的组件测试库，它是为用户提供对 Vue 特定 API 的访问而编写的。如果你对测试 Vue 应用不熟悉，我们建议你使用 Vue Testing Library，它是 Vue Test Utils 的抽象。

端到端测试虽然单元测试为开发者提供了一定程度的信心，但是单元测试和组件测试在部署到生产环境时提供应用整体覆盖的能力是有限的。因此，端到端测试可以说从应用最重要的方面进行测试覆盖：当用户实际使用应用时会发生什么。更全面,还能检测到后端代码

### TypeScript支持

### 生产环境部署

以下大多数内容在你使用 [Vue CLI](https://cli.vuejs.org/zh/) 时都是默认开启的。该章节仅跟你自定义的构建设置有关。

在 webpack 4+ 中，你可以使用 `mode` 选项：module.exports = {  mode: 'production' }

但是在 webpack 3 及其更低版本中，你需要使用 [DefinePlugin](https://webpack.js.org/plugins/define-plugin/)：

```
var webpack = require('webpack')

module.exports = {
  // ...
  plugins: [
    // ...
    new webpack.DefinePlugin({
      'process.env.NODE_ENV': JSON.stringify('production')
    })
  ]
}
```

模板预编译即使用 vue-template-loader

提取组件中的css,单文件组织内的CSS会以style标签通过js动态注入.这有一些小小的运行时开销，如果你使用服务端渲染，这会导致一段“无样式内容闪烁 (fouc)”。将所有组件的 CSS 提取到同一个文件可以避免这个问题，也会让 CSS 更好地进行压缩和缓存。https://vue-loader-v14.vuejs.org/zh-cn/configurations/extract-css.html

跟踪运行时错误在组件渲染时出现运行错误，错误将会被传递至全局 `Vue.config.errorHandler` 配置函数 (如果已设置)。利用这个钩子函数来配合错误跟踪服务是个不错的主意。比如 [Sentry](https://sentry.io/)，它为 Vue 提供了[官方集成](https://sentry.io/for/vue/)。

## 规模化

### 路由

 [vue-router 文档](https://router.vuejs.org/)。

### 状态管理

 [Vuex](https://github.com/vuejs/vuex)

### 服务端渲染

SSR https://ssr.vuejs.org/zh/

   [Nuxt.js](https://cn.vuejs.org/v2/guide/ssr.html#Nuxt-js)

### 安全

第一原则,不要使用用户自定义的html模板



 "editor.codeActionsOnSave": {

  "source.fixAll.eslint": true

 },