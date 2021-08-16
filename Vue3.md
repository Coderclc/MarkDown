# Vue3

1. $methods 为 提供的方法 _为非提供

2. object.defineproperty() 在浏览器的颜色会淡一点,是不可枚举的

3. 如果为(...) invoke property getter 即为设置了代理

4. vue 将_data的方法数据代理到vm上,将method的方法clone到vm上'

5. passive 用于移动端操作先执行默认行为 ' ,并不是所有的行为,少部分

6. 获取e.key,e.keyCode  将key(name) 转为.kebab-case

7. tab 在keyup的时候已经切走了光标,无法捕获,需要使用keydown

8. 系统修饰键 .ctrl .alt .shift .meta keyup必须要修饰其他案件,且在释放其他按键后触发,keydown直接触发

9. Vue.config.keyCodes  自定义keycodes

10. 如果页面没有发生改变,即使数据改变vuedevtools视图不会刷新

11. template 只会找vm上的,和原型不会去找全局作用域 但在js上可以把window放在data身上,

14. 旧虚拟dom和新虚拟dom之间进行diff算法对比,key相同的之间比较,相同保留,不相同重绘,input输入框的值是在 real dom上的 ,因为用index比较,又打乱了顺序,所以会出错,默认的使用“就地更新”的策略。不会移动dom 的顺序,而是就地更新,即为能复用就复用. 或者是刻意依赖默认行为以获取性能上的提升(有时候默认行为性能反而更好)。

    > `key` 的特殊 attribute 主要用在 Vue 的虚拟 DOM 算法，在新旧 nodes 对比时辨识 VNodes。如果不使用 key，Vue 会使用一种最大限度减少动态元素并且尽可能的尝试就地修改/复用相同类型元素的算法。而使用 key 时，它会基于 key 的变化重新排列元素顺序，并且会移除/销毁 key 不存在的元素。
    
15. call(thisArg[, arg1[, arg2[, ...]]])  bind(thisArg[, arg1[, arg2[, ...]]])([, arg1[, arg2[, ...]]])

    apply(thisArg, [argsArray])

    ```
        bar
        constructor(foo) {
            this.foo = foo
            this.bar = this.fun.bind(this)
        }
        xxx.bar() ✔
        const fn = xxx.bar  fn() ×
    ```

16. Sort

    使用[原地算法](https://en.wikipedia.org/wiki/In-place_algorithm)对数组的元素进行排序，并返回change数组。默认排序顺序是在将元素转换为字符串，比较UTF-16代码单元值序列(默认升序)

    - 如果 `compareFunction(a, b)` 小于 0 ，那么 a 会被排列到 b 之前；

    - 如果 `compareFunction(a, b)` 等于 0 ， a 和 b 的相对位置不变。备注： ECMAScript 标准并不保证这一行为，而且也不是所有浏览器都会遵守（例如 Mozilla 在 2003 年之前的版本）；

    - 如果 `compareFunction(a, b)` 大于 0 ， b 会被排列到 a 之前。(b本来就在a的前面,b为第n param a 为n+1)
    - `compareFunction(a, b)` 必须总是对相同的输入返回相同的比较结果，否则排序的结果将是不确定的。

    ```
     arr.sort((x, y) => x - y) // 若 compare > 0 则 x,y 交换位置 升序
     arr.sort((x, y) => y - x) // 若 compare < 0 则 x,y 位置不变 降序
    ```

    正数 0 不动,负数调换位置

    ```
     function getSort(fn) {
         return function (a, b) {
             let ret = 0
    
             if (fn.call(this, a, b)) { // a为第二参数 如果a>b为true 则返回-1调换位置,那么字面意义的a就大于b了
                 ret = -1
             } else if (fn.call(this, b, a)) {
                 ret = 1
             }
    
             return ret
         }
     }
    注: 必须返回正数 0 负数 才能排序, 若直接返回x>y 布尔值无效,希望这样书写,字面意义强借助getSort 转换
     function getMutipSort(arr) {
         return function (a, b) {
             let tmp
             let i = 0
    
             do {
                 tmp = arr[i++](a, b)  // 0 -1 1 
             } while (tmp === 0 && i < arr.length) // 如果为0且数组还有额外值,才继续exe,否则return
    
             return tmp
         }
     }
     
      arr.sort(
         getMutipSort([
             getSort((a, b) => a.time > b.time),
         ])
     )
    ```

17. easy data proxy

    ```
    function observer(obj) {
          const keys = Object.keys(obj)
      keys.forEach(k => {
            Object.defineProperty(this, k, {
          get() {
                return obj[k]
          },
              set(v) {
            obj[k] = v
              }
        })
          })
    }
    
    const obs = new observer(obj)
    ```

18. Vue.set(vm,key,value)  后添加observe  vm._data内的数据已被copy到了vm上(也可以操作数组)

    > ​	但避免追加一个响应式的属性到Vue的实例或者根节点的$data上,必须用于响应式对象上添加新的prop

19. 直接通过数组的索引值修改是无法修改数组的因为无get,set 但是数组内的对象有get,set,而数组的方法能够被vue检测到是因为这些方法被hook了,被包装(对象,数组,等任何数据类型初始化定义都有getter和setter,只有数组内的索引,和新添加的,删除的没有getter,setter)

20. 这样解释了为什么如果是getter的话,展示的数据为结果后的数据,因为都是在点击...的时候才重新获取,但如果console.log 到具体key就不同了,也解释了为什么我如果没有声明form.src就会导致src无法响应

21. `**Object.defineProperty()**` 方法会直接在一个对象上定义一个新属性，或者修改一个对象的现有属性，并返回此对象。无法劫持新增,删除数组的索引值,第一个参数只能是对象,p'roxy无敌,proxy deleteProperty监听删除

22. 同步队列 异步队列 作业队列

    ```
    consoloe.log('foo')
    setTimeout(() => {
    	console.log('bar')
    }, 0);
    new Promise(resolve =>
        resolve('resolve')	
    ).then(resolve => console.log(resolve)) 开启定时器,再将回调函数放到消息队列中,只有堆栈内无其他操作,才开始处理消息队列中的东西
    将Promise 放到作业队列中（即当前函数执行完后被立即执行）
    ```

    

23. > Vue 在更新 DOM 时是**异步**执行的。只要侦听到数据变化，Vue 将开启一个队列，并缓冲在同一事件循环中发生的所有数据变更。如果同一个 watcher 被多次触发，只会被推入到队列中一次。

    watch监听 有getter和setter才能触发watch , 但触发了watch不一定会刷新dom,如果首次渲染后的依赖列表里面没有该prop,即使触发了watch也不会更新dom,因为其不在依赖项列表(即在渲染过程中被访问的 property) 消息队列,作业队列的开启另外的watch, 同一个队列触发多次watch,，只会被推入到队列中一次。但是不同队列会推多次.
    
24. v-model checkbox 为数组即为添加删除value值,  为字符串,布尔即收集checked值

25. .numer 转为number 值 type=''number' 只能输入number

26. day.js 轻量化

27. document.cookie 拿到当前浏览器的所有cookie,除了httponly

28. console.dir print javaScript对象的属性，并通过类似文件树样式的交互列表显示

29. dom对象 instanceof HTMLElement  检测真实dom

30. 自定义指令`update`：所在组件的 VNode 更新时调用，**但是可能发生在其子 VNode 更新之前**。指令的值可能发生了改变，也可能没有。但是你可以通过比较更新前后的值来忽略不必要的模板更新  ,自定义指令的值该发生在dom tree update 而非单一bind value change

31. html 阻塞 即从上到下按顺序加载并且执行

    - defer 异步加载dom解析完成以后执行
    - async 异步加载并执行(执行的过程中会影响dom解析)
    - ![wfL82.png](https://segmentfault.com/img/bVWhRl?w=801&h=814
    
32. 在bind执行类似foucus,parentnode is invalid ,此时dom还未成功挂载,需要在insert中

33. 因为切换eye导致input type change vdom refresh,此时刷新后的input与focus同时,须在nexttick执行,且mousedown为focus ,mouseup为click 

34. beforeCreated 数据代理数据监测之前此时debugger无coder自定义内容,data,method

35. template 选项会整个替换div#app,而el,mouted只是挂载

36. beforeUpdate 数据是新的页面是旧的,接下来 Virtual DOM re-render and patch

37. vm.$destory()  beforeDestroy() destroyed() 里的getter不会才更新视图 ,一种是移除销毁,一直是调方法销毁,二者皆为解绑指令,移除事件监听,并不是真正意义上的销毁

    > 在大多数场景中你不应该调用这个方法。最好使用 `v-if` 和 `v-for` 指令以数据驱动的方式控制子组件的生命周期。

38.  this.$forceUpdate() 之前我认为的是调update() 逻辑错了,应该是强制刷新dom,更新一些无getter触发的dom,虚拟dom patch 会触发update

39. Vue.extend 创建组件构造器 模板来源于 template 选项 或者template 标签,使用的时候,在局部注册挂载, 或者new 一个实例$mounted

40. vue devtools 名字取决于选项名字

41. 在非.vue ,标签首字母会被html转换为小写,其余不会转换,html模板无法识别大写

42. Vue.extend 生产的是组件构造函数,组件构造器 1.手动new construction()2.写</> Vue会帮我们new一个实例对象 注册执行Vue.extend,一个实例标签一个 new

43. 组件构造器的原型是一个Vue的实例,组件构造器的显示原型的隐示原型指向Vue的显示原型,采用Object.create

44. index.html

    - noscript 不支持js

    -  <meta http-equiv="X-UA-Compatible" content="IE=edge">
      针对ie的配置,使其使用最高级别的渲染级别渲染页面

    - <meta name="viewport" content="width=device-width,initial-scale=1.0">
      开启移动端的理想视口
    
45. vue-template-compiler 解析.vue 的template

46. 找node_modules下同名的包,再根据文件内的package.json的"module":,找到js文件,如果没有main,则找文件夹内的index.js,找不到就在node的上一级找,直到磁盘根目录.main有意外暴露内容的风险

47. 查看vue的所有配置项目 vue inspect > output.js

48. npm view package versions    npm init vite@latest

49. id不会用number类型, 因为number类型是有尽头的

50. uuid 全球唯一字符串编码,1日期时间2.时钟序列3,全局唯一的IEEE机器识别号

    nanoid  uuid一定程度的缩减

49. prop可以是一个函数,那么子组件可以通过prop函数传递数据,prop 只有改变基本数据类型和引用数据类型地址才会报错,其余不报错

50. v-model 一个计算属性就不用写@change了例如checkbox上

51. window上的方法是直接暴露出来的!!!!!!!!!!!!!!

52. 1.获取 dom 添加onclick 事件  2.直接在元素上声明onclick="onClick()" 必须带小括号

53. localStorage setItem 第二个参数为非string形式会执行toString 方法

54. localStorage setItem getItem removeItem clear()

55. vm.$refs.cpn.$on('test', function (msg) {  console.log(msg) }) 手动监听自定义事件

56. 因为destroy() 会teardown watchers child components and event listeners 销毁会拆解自定义事件,无论是@还是 $on绑定的事件都会被拆解,$off可以在指定的时候teardown,且都能拆

57. $emit 和$on必须是同一个实例 且$on 的function 回调this不是window而是触发的实例

58. 可在vue.beforeCreate之前添加$bus

59. $set 就可以不用初始化添加一些例如isEdit = false 这种数据了 完美一点使用hasOwnProperty''防止重复$set

60. 动画在active 过渡在to leave

61. axios $ajax 基于xhr 封装 fetch 地位相对于xhr,返回两层promise

62. CORS 要求协议 主机端口相同 1.后端配置cors 2. jsonp 返回一个执行同名函数 3. 代理服务器,服务之间无跨域问题

63. devServer proxy 执行后端,本地请求指向本机代理,1.本地已有不会转发2.无法配置多个,1.字符串public已有不转发否则转发 

64. 避免以上情况 使用 [http-proxy-middleware](https://github.com/chimurai/http-proxy-middleware#proxycontext-config) . ,配置前缀,为转发,否则不转发,转发会把前缀也带上,需要不在官网的配置   pathRewrite: {'^/api': '' }, ws proxy websockets ,  changeOrigin: false, 伪装 true伪装成服务器端口

65. 插槽的作用域为父,但样式作用域为父子

66. 插槽相同名字为累加而非覆盖.

67. \&nbsp;空格

##  Change

1. monorepo 管理 
   - mono 单个,repo repository仓库
   - 多个包之间相互独立,有自己的功能逻辑,单元测试,同一个仓库下方便管理
   - 模块划分清晰,可维护性,可拓展性强
2. Vue3改用es6的Proxy实现劫持
   - Vue2.x使用的Object.defineProperty来劫持obj的getter和setter,缺陷是设置和删除无法劫持,所以用相应的hack方法api$delete,$set,
3. 删除了一些不必要的api
   - 删除了$on,$off,$once,
   - 移除了filter,内联模板inline-template(在父组件中声明的数据和子组件中声明的数据两个都可以渲染,这反而是缺点)等
4. 编译方面的优化
   - 生成block tree ,slot编译优化,diff算法优化
5. 由Options API到Composition Api
   - 在Vue2.x通过Options API来描述组件对象,包括 data,props,methods,computed,生命周期等选项,问题在于多个逻辑可能实在不同的地方,跳来跳去?
   - composition API 可以将相关联的代码放到同一行进行处理,而不需要在多个Options之间寻找
6. Hooks 函数增加代码的复用性
   - Vue2.x使用mixins来共享组件逻辑,缺陷在于mixins也使由Options组成的,多个mixins会存在命名冲突的问题,
   - 3.x可以通过hook函数,将一部分独立的逻辑抽取出去,并且还能做到是响应式的![script](C:\Users\Coderclc\Documents\MarkDown\images\script.webp)



# Vue3

vue 2.2

new Vue({}).$mount('#app')

vue.3

Vue.createApp({}).mount('#app')

- 应用实例暴露的大多数方法都会返回该同一实例，允许链式：

```
Vue.createApp({})
  .component('SearchInput', SearchInputComponent)
  .directive('focus', FocusDirective)
  .use(LocalePlugin)
```

与大多数应用方法不同的是，`mount` 不返回应用本身。相反，它返回的是根组件实例。

```
const RootComponent = { /* 选项 */ }
const app = Vue.createApp(RootComponent)
const vm = app.mount('#app')
```

- destroyed --> unmounted  beforeDestroy --> beforeUnmount

- Lodash 的debounce 和 `throttle` 防止组件复用,应该在created或者mounted中赋予

- style对象的vendor prefix多重值

  ```
  <div :style="{ display: ['-webkit-box', '-ms-flexbox', 'flex'] }"></div>
  ```

  这样写只会渲染数组中最后一个被浏览器支持的值。在本例中，如果浏览器支持不带浏览器前缀的 flexbox，那么就只会渲染 `display: flex`。

- `v-show` 不支持 `<template>` 元素，也不支持 `v-else`。 本质为display:none

- ``` html
  v-for="value in myObject"  遍历对象
  v-for="(value, key,index) in myObject" value ,key,index
  ```

  > 在遍历对象时，会按 `Object.keys()` 的结果遍历，但不能保证在不同 JavaScript 引擎下的结果都一致。

- v-on 多事件处理器
-  @click="one($event), two($event)" 执行两个方法 必须为event() event无效

-    .capture 在冒泡排序中先捕获

  - 默认有里向外冒泡 有.captrue 优先 全部都有.captrue 向下冒
  - 冒泡是从里往外冒，捕获是从外往里捕。
  - 当捕获存在时，先从外到里的捕获，剩下的从里到外的冒泡输出。
  - @click.stop 只有事件修饰符,用于阻止冒泡

- `v-on:click.prevent.self` 会阻止所有的点击，而 `v-on:click.self.prevent` 只会阻止对元素自身的点击。

- .passive

  - 【浏览器只有等内核线程执行到事件监听器对应的JavaScript代码时，才能知道内部是否会调用preventDefault函数来阻止事件的默认行为，所以浏览器本身是没有办法对这种场景进行优化的。这种场景下，用户的手势事件无法快速产生，会导致页面无法快速执行滑动逻辑，从而让用户感觉到页面卡顿。】 通俗点说就是每次事件产生，浏览器都会去查询一下是否有preventDefault阻止该次事件的默认动作。我们加上**passive就是为了告诉浏览器，不用查询了，我们没用preventDefault阻止默认动作。**

    > 不要把 `.passive` 和 `.prevent` 一起使用，因为 `.prevent` 将会被忽略，同时浏览器可能会向你展示一个警告。请记住，`.passive` 会告诉浏览器你*不想*阻止事件的默认行为。

- 系统修饰符 .ctrl .alt .shift .meta `.exact` 修饰符 精确

- `v-model` 在内部为不同的输入元素使用不同的 property 并抛出不同的事件：

- text 和 textarea 元素使用 `value` property 和 `input` 事件；

- checkbox 和 radio 使用 `checked` property 和 `change` 事件；

- select 字段将 `value` 作为 prop 并将 `change` 作为事件。

  > Note
  >
  > 如果 `v-model` 表达式的初始值未能匹配任何选项，`<select>` 元素将被渲染为“未选中”状态。在 iOS 中，这会使用户无法选择第一个选项。因为这样的情况下，iOS 不会触发 `change` 事件。因此，更推荐像上面这样提供一个值为空的禁用选项。

```
  <select v-model="selected">
    <option disabled value="">Please select one</option>
    <option>A</option>
    <option>B</option>
    <option>C</option>
  </select>
```

- 类似props 一样 定义 emits: ['in-focus', 'submit'] 但不是必须的

  > 建议定义所有发出的事件，以便更好地记录组件应该如何工作。

- 验证抛出的事件

  ```
   emits: {
      // 没有验证
      click: null,
  
      // 验证submit 事件
      submit: ({ email, password }) => {
        if (email && password) {
          return true
        } else {
          console.warn('Invalid submit event payload!')
          return false
          // 将会抛出一个warning
          vue@next:1312 [Vue warn]: Invalid event arguments: event validation failed for 			event "click".
        }
      }
    },
  ```

- 在组件上使用 v-model

  -  vue 2.2 

    ```
    <custom-input
      v-bind:value="searchText"
      v-on:input="searchText = $event"
    ></custom-input>
    ```

  - vue 3.0  ! model失效

    ```
    <custom-input
      :model-value="searchText"
      @update:model-value="searchText = $event"
    ></custom-input>
    ```

  tips  使用计算属性重构 `<custom-input>` 组件

  ```js
      get() {
          return this.modelValue
      },
      set(value) { 
          this.$emit('update:modelValue', value)
      }
  ```



- 动态组件

   Vue 的<component :is="currentTabComponent" />

  在上述示例中，`currentTabComponent` 可以包括

  - 已注册组件的名字，或 全局?
  - 一个组件的选项对象

- .prop

  > 请留意，这个 attribute 可以用于常规 HTML 元素，但这些元素将被视为组件，这意味着所有的 attribute **都会作为 DOM attribute 被绑定**。对于像 `value` 这样的 property，若想让其如预期般工作，你需要使用 [.prop 修饰器](https://vue3js.cn/docs/zh/api/directives.html#v-bind)。 https://segmentfault.com/a/1190000012820563

- v-is

```html
<table>
  <blog-post-row></blog-post-row>
</table>
会被作为无效的内容提升到外部，并导致最终渲染结果出错。幸好这个特殊的 v-is attribute 给了我们一个变通的办法：跑到table外了
```

```
<table>
  <tr v-is="'blog-post-row'"></tr>
</table>
v-is 值应为 JavaScript 字符串文本：
即组件字符串
```

- HTML 属性名不区分大小写，因此浏览器将把所有大写字符解释为小写。这意味着当你在 DOM 模板中使用时，驼峰 prop 名称和 event 处理器参数需要使用它们的 kebab-cased (横线字符分隔) 等效值：
  - 需要注意的是**如果我们从以下来源使用模板的话，这条限制是\*不存在\*的**：
    - 字符串模板 (例如：`template: '...'`)
    - [单文件组件](https://vue3js.cn/docs/zh/guide/single-file-component.html)
    - `<script type="text/x-template">`

- 烈推荐遵循 [W3C 规范](https://html.spec.whatwg.org/multipage/custom-elements.html#valid-custom-element-name)中的自定义组件名 (字母全小写且必须包含一个连字符)

- Prop 提示

  注意在 JavaScript 中对象和数组是通过引用传入的，所以对于一个数组或对象类型的 prop 来说，在子组件中改变变更这个对象或数组本身**将会**影响到父组件的状态

  -  传的是对象或数组内存地址, ,1. 直接修改不会报错  2. 传moment这种对象类型会导致子组件修改父组件

- ```js
  // 基础的类型检查 (`null` 和 `undefined` 会通过任何类型验证)
  印象之中会报null错误?
  ```

- ```js
  // 自定义验证函数
  propF: {
    validator: function(value) {
      // 这个值必须匹配下列字符串中的一个
      return ['success', 'warning', 'danger'].indexOf(value) !== -1
    }
  },
  // 具有默认值的函数
  propG: {
    type: Function,
    // 与对象或数组默认值不同，这不是一个工厂函数 —— 这是一个用作默认值的函数
    default: function() {
      return 'Default function'
    }
  }
  ```

- prop 和 event 将会继承与根节点
  - 2.x  无法继承event  需要@click.native  或者子组件 on={this.$listeners}
  - 3.x  移除 直接继承

- 禁用 inheritAttrs: false

  - 禁用 attribute 继承的常见情况是需要将 attribute 应用于根节点之外的其他元素
  - 也就是防止prop 或者$attr 对根组件的影响
  - 通过将 `inheritAttrs` 选项设置为 `false`，你可以访问组件的 `$attrs` property，该 property 包括组件 `props` 和 `emits` property 中未包含的所有属性 (例如，`class`、`style`、`v-on` 监听器等)。
  - 将$listeners 移到了$attrs  ,使用 v-bind="$attrs" 建议最好要把 inheritAttrs: false,带上,
  - 事件也是v-bind=$attrs 而非v-on='$listeners'
  
- 多个根节点, 现在可以是多个根节点了
  - 不具有自动 attribute 回退行为。如果未显式绑定 `$attrs`，将发出运行时警告。
  
- 在dom模板中@myEvent 无法接受到 emit('myEvent') 需为@my-event

- 推荐你始终使用 **kebab-case 的事件名**

- 当在 `emits` 选项中定义了原生事件 (如 `click`) 时，将使用组件中的事件**替代**原生事件侦听器。指的是例如click事件将无法click触发,而是只能由emit触发

- mode 替换  默认情况下，组件上的 `v-model` 使用 `modelValue` 作为 prop 和 `update:modelValue` 作为事件。我们可以通过向 `v-model` 传递参数来修改这些名称： v-model:foo  :value='foo'  update:foo

- 多个v-model 绑定

  - ```
    <user-name
      v-model:first-name="firstName"
      v-model:last-name="lastName"
    ></user-name>
    然后 props  emits 分别声明
    ```

- v-model 修饰符

  - 内置修饰符 .trim`、`.number` 和 `.lazy

  - 自定义修饰符 通过prop modelModifiers

    ```
    在html 片段中  <div modelvalue="123" modelmodifiers="[object Object]">
    ```

  - 请注意，当组件的 `created` 生命周期钩子触发时，`modelModifiers` prop 包含 `自定义修饰符名`，其值为 `true`——因为它被设置在 `v-model` 绑定 `v-model.capitalize="bar"`。

    ```
      props: {
        modelValue: String,
        modelModifiers: {
          default: () => ({})
        }
      },
      带参数的v-model 生成的 prop 名称将为 arg + "Modifiers"：
    在prop 中可获得自定义属性名为一个对象如果modelValue 为 foo 那么modelModifiers-fooModifiers
    v-model.number => {number:true}
    v-model.a.b.c.d   =>  {a,b,c,d = true}
    ```

- $attrs 包含不在props中的 attr 和emits 中的event

- slot

  > 父级模板里的所有内容都是在父级作用域中编译的；子模板里的所有内容都是在子作用域中编译的

  虽然是插入子作用域,确实在父作用域编译的

  - 后备内容 ,即插槽的default value

  - 具名  name =''  v-slot:  #default

  - 2.2 之前是 slot='' slot-scope=''

  - **`v-slot` 只能添加在 `<template>` 上** ([只有一种例外情况](https://vue3js.cn/docs/zh/guide/component-slots.html#独占默认插槽的缩写语法)) 那就是只有默认插槽并且需要作用域插槽的时候,其余情况需要插槽都给我把template 加上

  - ``` 
    v-slot:default="slotProps"
    可以缩写成 v-slot='obj' 2.2不
    ```

- provide

  ```
  provide:{
   	user :CONST
  }
  provide(){
  	return {
  		???:???
  	}
  }
  ```

  -  处理响应式 ,provde 在vue2.2是耦合的并且非响应式的
    - ['ARRLENGTH']: Vue.computed(() => this.arr.length) 那么inject ARRLENGTH 变成ARRLENGTH.value并且具有响应式

- 异步组件

  ```
  const app = Vue.createApp({}) 必须要传一个对象 
  const AsyncComp = Vue.defineAsyncComponent(
    () =>
      new Promise((resolve, reject) => {
        resolve({
          template: '<div>I am async!</div>'
        })
      })
  )
  app.component('async-example', AsyncComp)
  ```

  ```
    components: {
     AsyncComponent: defineAsyncComponent(()=>import('./components/AsyncComponent.vue'))
    }
  ```

  defineAsyncComponent 此方法接受返回 `Promise` 的工厂函数 而// 这个动态导入会返回一个 `Promise` 对象。  () => import('./my-async-component')  import()

  > 当某个组件文件很大的时候,可以用懒加载进行code-spliting 切割,构建后，任何动态导入的组件都会作为一个单独的文件。当需要的时候,就会从服务器请求这个组件,如果该组件非常大的时候,页面渲染就会出现停顿

  -  与 Suspense 一起使用 

    > <Suspense> is an experimental feature and its API will likely change.
    >
    > 还是实验性的功能

    异步组件在默认情况下是可挂起的。这意味着如果它在父链中有一个 `<Suspense>`，它将被视为该 `<Suspense>` 的异步依赖。在这种情况下，加载状态将由 `<Suspense>` 控制，组件自身的加载、错误、延迟和超时选项将被忽略。

    异步组件可以选择退出 `Suspense` 控制，并通过在其选项中指定 `suspensable:false`，让组件始终控制自己的加载状态。

    你可以在中查看可用选项的列表 [API 参考](https://vue3js.cn/docs/zh/api/global-api.html#arguments-4)

当 `ref` 与 `v-for` 一起使用时，你得到的 `ref` 将是一个数组，其中包含镜像数据源的子组件。

但是不在是这种写法了 https://vue3js.cn/docs/zh/guide/migration/array-refs.html

- 边界情况

- $forceUpdate :迫使组件实例重新渲染。注意它仅仅影响实例本身和插入插槽内容的子组件，而不是所有子组件。其实是强制执行生命周期中的update

- v-once 用于大量的静态html文本

-  [CSS Triggers](https://csstriggers.com/) 来查看哪些属性会在动画时触发重绘,也就是说有一些属性是需要浏览器重新布局并且重绘,而避免重绘可以在 web 上创建极其流畅的动画

- CSS perspective 属性 perspective 属性定义 3D 元素距视图的距离，以像素计。该属性允许您改变 3D 元素查看 3D 元素的视图。用于3d视图

- 硬件加速,强制开启某些元素的硬件加速,例如

  ```
  perspective: 1000px;
  backface-visibility: hidden;
  transform: translateZ(0);
  貌似相似hack 方法处理bfc
  ```

- CSS 允许你通过调整 cubic bezier 属性来修改 Easing，Lea Verou 开发的[这个 playground](https://cubic-bezier.com/#.17,.67,.83,.67) 对探索这个问题非常有帮助。
- transition
  1. 自动嗅探目标元素是否应用了 CSS 过渡或动画，如果是，在恰当的时机添加/删除 CSS 类名。
  2. 如果过渡组件提供了 [JavaScript 钩子函数](https://vue3js.cn/docs/zh/guide/transitions-enterleave.html#javascript-hooks) ，这些钩子函数将在恰当的时机被调用。
  3. 如果没有找到 JavaScript 钩子并且也没有检测到 CSS 过渡/动画，DOM 操作 (插入/删除) 在下一帧中立即执行。(注意：此指浏览器逐帧动画机制，和 Vue 的 `nextTick` 概念不同)
- css 过渡,也就是常规的操控triggers属性 css 动画也就是操作 anmation区别在于过渡的v-enter-from会在dom插入下一帧移除, 而动画` v-enter-from` 类名在节点插入 DOM 后不会立即删除，而是在 `animationend` 事件触发时删除。
- 自定义过渡类名 用于导入第三方库.css

-  JavaScript 钩子  例如@before-enter="beforeEnter" 函数 使用第三方的 动画js库
- 使用钩子的时候注意,在 **`enter` 和 `leave` 钩中必须使用 `done` 进行回调**。否则，它们将被同步调用，过渡会立即完成。添加 `:css="false"`，也会让 Vue 会跳过 CSS 的检测，除了性能略高之外，这可以避免过渡过程中 CSS 规则的影响。
- 初始渲染的过渡可以通过 `appear` attribute 设置节点在初始渲染的过渡,可用自定义类名或者钩子

- 过渡模式 单个元素过渡无需, 多个元素之间过渡,也只是过渡一个元素.一个离开过渡的时候另一个开始进入过渡,多个元素过渡的key值必须不同否则不会执行

  > 很快就会发现 `out-in` 是你大多数时候想要的状态 😃

- 多个组件过渡 

  ```html
    <transition name="component-fade" mode="out-in">
      <component :is="view"></component>
    </transition>
  ```

- 列表过渡

  - 不同于 `<transition>`，它会以一个真实元素渲染：默认为一个 `<span>`。你也可以通过 `tag` attribute 更换为其他元素。

  - 必须要有key

  - 过渡的类应用的是组的内部元素而非容器本身

  - 这里有一点很奇怪的是为了实现FILP动画 ,原本加载进入和离开的过渡transtion必须加载元素上,(因为原本需要加载active和move,现在直接加在state 状态)并且leave-active需要加上 postion absolute

  - ```
    .list-item {
      display: inline-block;
    }
    .list-enter-active,
    .list-leave-active {
      transition: all 1s ease;
    }
    .list-leave-active {
      position: absolute;
    }
    .list-enter-from,
    .list-leave-to {
      opacity: 0;
      transform: translateY(30px);
    } 
    .list-move {
      transition: transform 0.8s ease;
    }
    较好的方案
    ```

    

  > 需要注意的是使用 FLIP 过渡的元素不能设置为 `display: inline`。作为替代方案，可以设置为 `display: inline-block` 或者放置于 flex 中

- mixins 

  - 据对象在内部会进行递归合并，并在发生冲突时以组件数据优先。
  - 同名钩子函数将合并为一个数组，因此都将被调用。另外，混入对象的钩子将在组件自身钩子**之前**调用

  - 自定义选项合并策略(改变合并策略,没必要没必要)
  - 在vue2中mixins有几个问题第一,mixin很容易发生冲突第二,可重用性是有限的,我们不能向mixin传递任何参数来改变他的逻辑 ->组合式api

- directive

  - 包含以下几个钩子函数beforeMount,mounted,beforeUpdate,updated,beforeUnmount,unmounted
  - 你可能想在 `mounted` 和 `updated` 时触发相同行为，而不关心其它的钩子。比如这样写：指令名后面直接加函数(不用拆开写两个相同的,写一个即可)

- teleport

  - 逻辑属于组件,但是技术角度上最好移到dom,比如那些popver?

  - ```html
    <teleport to="body"></teleport>
    ```

  > 在这种情况下，即使在不同的地方渲染 `child-component`，它仍将是 `parent-component` 的子级，并将从中接收 `name` prop。
  >
  > 在vue-tools 中位置与仍在嵌套原处,dom上teleport 到了 body

  多个传送时后挂载的在前面之后

  > warn 无法使用选择器“#modals”定位传送目标。 请注意，目标元素必须在组件挂载之前存在 - 即目标不能由组件本身呈现，理想情况下应该在整个 Vue 组件树之外。不能在自己内部teleport 必须是已经在组件树的vnode

- 渲染函数

  - import { createVNode as h,h } from 'vue';

  - 移除[$scopedSlots](https://cn.vuejs.org/v2/api/#vm-scopedSlots)合并为this.$slots.default()

  - Vue 通过建立一个**虚拟 DOM** 来追踪自己要如何改变真实 DOM。 return Vue.h('h1', {}, this.blogTitle)

  - 可选的第二个参数{Object} props却报错了(大部分都写null)

  - VNODE 必须唯一,所以 重复的时候需要用工厂函数来进行渲染

    ```
    render() {
      return Vue.h('div',
        Array.apply(null, { length: 20 }).map(() => {
          return Vue.h('p', 'hi')
        })
      )
    }
    ```

  - v-if ,v-for

  - v-model

    ```
    c{
        modelValue: this.modelValue,
        'onUpdate:modelValue': value => this.$emit('update:modelValue', value)
      }
    ```


- vue2.2 实现自定义插件

  ```
  const toast = Vue.extend(Toast) 得到组件构造器 
  Vue.component('toast',toast)
  语法糖  Vue.component('toast',Toast) 直接置组件选项对象,平时我的局部注册就是组件祖册的语法糖
  ```
  
  ```
  import Toast from './index.vue'  // 组件选项对象
  const zoe = {} 
  let toast
  zoe.install = Vue => {
    const ToastConstructor = Vue.extend(Toast) // 得到组件构造器类
    toast = new ToastConstructor() 得到vue 的实例
    toast.$mount(document.createElement('div')) 该方法在Vue的原型上,根组件app也是如此挂载,此时还没有$el,必须挂载在一个el上才有,才能挂在dom上(参考生命周期mounted执行完毕以后$el代替el)
    document.body.appendChild(toast.$el) 直接
    Vue.prototype.$toast = toast
  }
  export default zoe
  export {
    toast
  }
  Vue.use zoe 这个对象会执行对象的install 方法
  ```
  
- vue3.0 plugin


  - 插件是自包含的代码，通常向 Vue 添加全局级功能。它可以是公开 `install()` 方法的 `object`，也可以是 `function`
    1. 添加全局方法或者 property。如：[vue-custom-element](https://github.com/karol-f/vue-custom-element)
    2. 添加全局资源：指令/过滤器/过渡等。如：[vue-touch](https://github.com/vuejs/vue-touch)）
    3. 通过全局 mixin 来添加一些组件选项。(如[vue-router](https://github.com/vuejs/vue-router))
    4. 添加全局实例方法，通过把它们添加到 `config.globalProperties` 上实现。
    5. 一个库，提供自己的 API，同时提供上面提到的一个或多个功能。如 [vue-router](https://github.com/vuejs/vue-router)

  - 每当这个插件被添加到应用程序中时，如果它是一个对象，就会调用 `install` 方法。如果它是一个 `function`，则函数本身将被调用。在这两种情况下——它都会收到两个参数：由 Vue 的 `createApp` 生成的 `app` 对象和用户传入的选项(不是Vue 而是vue的实例,对象为) app.use的第二个选项

  - 注意(vue2.2为第一个参数为Vue构造器) 可以为函数 不用起对象名字了

  - vue2.2 为Vue.use  vue3.0为app.use

- 把函数添加到 app.config.globalProperties 上变成全局方法

- ```js
    app.provide('i18n', options) 子组件通过inject 'i18n'
  还有app.mixin  app.directive
  ```

- ```
  export default app => {
      const toast = createApp(Toast)
  
      const el = document.createElement('div')
      document.body.appendChild(el)
  
      toast.mount(el)
  
      app.provide('toast', toast)
      app.config.globalProperties.$toast = toast
  
  }
  ```
  
- 深入响应式原理


    - Vue 会使用带有 getter 和 setter 的处理程序遍历其所有 property 并将其转换为 [Proxy](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy)。这是 ES6 仅有的特性，使用了 `Object.defineProperty` 来支持 IE 浏览器。两者具有相同的 Surface API，但是 Proxy 版本更精简，提升了性能。

- reflect 与 proxy


    - proxy: 通过get和set对对象代理操作,可在过程中添加一些额外的操作
    - reflect 可以用于获取目标对象的行为，它与 Object 类似，但是更易读，为操作对象提供了一种更优雅的方式。它的方法与 Proxy 是对应的。
    - 通过构造函数新建实例时其实是对目标对象进行了浅拷贝，因此目标对象与代理对象会互相 // 影响,也就是proxy.name = '' 会影响target
    - // handler 对象也可以为空，相当于不设置拦截操作，直接访问目标对象 就没啥区别了和obj
    -  get(target, propKey, receiver) target 和propKey 指向同一个对象
    - set:(target, propKey, value, receiver) 
    
    - (new class 出来的对象.\___proto\___ 指向class 的prototype, 而正常的obj为Object: null prototype空原型,通过)`Object.create()`方法创建一个新对象，使用现有的对象来提供新创建的对象的__proto__。.(tm的意思就是新对象的原型指向旧对象,新对象的基本数据类型拷贝了一份,引用数据类型没有拷贝,所以使用拷贝对象方法实际是使用继承的也是原型上的方法)
    
    - ```
      let proxy = new Proxy({}, {
        get(target, propKey, receiver) {
            // 实现私有属性读取保护
            if(propKey[0] === '_'){
                throw new Erro(`Invalid attempt to get private     "${propKey}"`);
            }
            console.log('Getting ' + propKey);
            return target[propKey];
        }
      });
       
      let obj = Object.create(proxy);
      obj.name
      // Getting name  get 也是可继承的
      ```
    
    - ```
      Object.setPrototypeOf(obj, prototype) 吧prototype设置到obj的__proto__
      ```
    
    - ```
      const obj = {
        log: ['a', 'b', 'c'],
        get latest() {
          if (this.log.length === 0) {
            return undefined;
          }
          return this.log[this.log.length - 1];
        }
      };
      
      console.log(obj.latest);
      对象的get 方法 如果没有get  需要执行 obj.latest()
      ```
    
    - ```
      const language = {
        set current(name) {
          this.log.push(name);
        },
        log: []
      }
      
      language.current = 'EN';
      console.log(language.log); // ['EN']
      
      language.current = 'FA';
      console.log(language.log); // ['EN', 'FA']
      对象的set 方法
      ```
    
      ```js
      Reflect.get(...arguments) Reflect.get(target, name, receiver) 当target中有get 方法也就是上述的对象的get方式时,this会指向receiver Reflect.set(...arguments)同理
      ```

- Vue 在get 方法执行了   effect track(target, prop)  在set 方法执行 trigger(target, key)
- Vue 如何处理这些更改的答案
  - ~~当某个值发生变化时进行检测~~：我们不再需要这样做，因为 Proxy 允许我们拦截它
  - **跟踪更改它的函数**：我们在 Proxy 中的 getter 中执行此操作，称为 `effect`
  - **触发函数以便它可以更新最终值**：我们在 Proxy 中的 setter 中进行该操作，名为 `trigger`

- Vue 在内部跟踪所有已被设置为响应式的对象，因此它始终会返回同一个对象的 Proxy 版本。所有的data等的对象都会被proxy代理

- ```
     const foo = {}
     const bar = foo
     console.log(foo===bar); true
     但是proxy带来一个问题即target === proxy  false 虽然行为相同,即修改proxy 会修改target 但是赖严格比对是失败的 比如filter和map 他们的返回 truthy 必须为===
  ```

- 每个组件实例都有一个相应的侦听器实例，该实例将在组件渲染期间把“触碰”的所有 property 记录为依赖项。之后，当触发依赖项的 setter 时，它会通知侦听器，从而使得组件重新渲染。首次渲染后，组件将跟踪一组依赖列表——即在渲染过程中被访问的 property。反过来，组件就成为了其每个 property 的订阅者。当 Proxy 拦截到 set 操作时，该 property 将通知其所有订阅的组件重新渲染。

- 每一个组件都有一个侦听器,实例将在组件渲染期间把“触碰”的所有 property 记录为依赖项。多对多的关系,反过来侦听器为pro的订阅者,当proxy拦截到了prop的trigger操作的时候, prop会通知所有的订阅者重新渲染

- 响应式基础

  - reactive  响应式对象

  - ref 响应式值 

  - 当 `ref` 作为响应式对象的 property 被访问或更改时自动展开为value

    ```
    ref =  0  state{ref}
    state.ref = 1  并不是修改state.ref 而是修改state.ref.value
    ref = 1
    
    ref = 0  state[ref]
    state[0] = 1   / /Array  或者map不会展开
    ref = 0
    ```

  - toRefs 直接解构的两个 property 的响应性都会丢失。对于这种情况，我们需要将我们的响应式对象转换为一组 ref。这些 ref 将保留与源对象的响应式关联：

    ```
    let { author, title } = toRefs(book)
    
    title.value = 'Vue 3 Detailed Guide' // 我们需要使用 .value 作为标题，现在是 ref
    console.log(book.title) // 'Vue 3 Detailed Guide'
    ```

  - readonly

    ```
    import { reactive, readonly } from 'vue'
    const original = reactive({ count: 0 })
    const copy = readonly(original)
    // 在copy上转换original 会触发侦听器依赖
    original.count++
    // 转换copy 将导失败并导致警告
    copy.count++ // 警告: "Set operation on key 'count' failed: target is readonly."
    ```

- 响应式计算和侦听

  - computed

  - ```
    const count = ref(1)
    const plusOne = computed(() => count.value++)
    console.log(plusOne.value) // 2
    
    plusOne.value++ // error  只有get 无法操作
    ```

    ```
    const count = ref(1)
    const plusOne = computed({
      get: () => count.value + 1,
      set: val => {
        count.value = val - 1
      }
    })
    
    plusOne.value = 1
    console.log(count.value) // 0
    ```

  - watchEffect

    ```
    const count = ref(0)
    watchEffect(() => console.log(count.value))
    // -> logs 0
    setTimeout(() => {
      count.value++
      // -> logs 1
    }, 100)
    ```

    ```
    侦听器会被链接到该组件的生命周期，并在组件卸载时自动停止。 會自動停止,也可以手動t
    const stop = watchEffect(() => {
      /* ... */
    })
    // later
    stop()
    ```

    
