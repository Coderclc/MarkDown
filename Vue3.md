# Vue3

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
   - 生成block tree ,slot编译优化,diff算法优化,打包大小减少41%,初次渲染快了55%,更新渲染快133%,内存减少54%
   - 冲重写虚拟DOM的实现和实现更好的tree-shaking
5. 由Options API到Composition Api
   - 在Vue2.x通过Options API来描述组件对象,包括 data,props,methods,computed,生命周期等选项,问题在于多个逻辑可能实在不同的地方,跳来跳去?
   - composition API 可以将相关联的代码放到同一行进行处理,而不需要在多个Options之间寻找
6. Hooks 函数增加代码的复用性
   - Vue2.x使用mixins来共享组件逻辑,缺陷在于mixins也使由Options组成的,多个mixins会存在命名冲突的问题,
   - 3.x可以通过hook函数,将一部分独立的逻辑抽取出去,并且还能做到是响应式的![script](C:\Users\Coderclc\Documents\MarkDown\images\script.webp)
7. 拥抱ts
8. vite 上来就server ready 其次请求再分析依赖
9. const app = createApp(App) 更轻了
10. setup
    - 新的配置项 是一个在所有生命周期之前的函数(所以没有this)
    - 返回对象则用于模板中使用,或者直接返回render函数()=>(\<section>\</section>)
    - 尽量不要混这些,vue2.x中可以访问setup中的属性和方法,反过来不行,没有this
    - 如果重名,setup优先 object.assign
    - 不想写根就用<></>来写
11. refImpl reference implement 引用实现 在模板中自动展开.value ,render不会自动展开返回引用实现的实例
12. ref 代理基本数据类型用的object.define,引用用的proxy,reactive 代理用的proxy, ref代理对象其实就是使用了ref(reactive())
13. ref中的普通对象会被转换成proxy,通过.value访问,
14. 读取proxy key中的 refImpl 会自动展开value,index值不会自动展开
15. ref(ref()) reactive(reactive()) 返回自身  ref(reactive()) reactive(ref())返回ref 
16. delete 这个关键字是有返回值的,比如删除无配置不可枚举的对象key值会返回false
17. Object,defineProperty can't redefine  Reflect.defineProperty可以
18. Reflect.defineProperty有返回布尔值表示代理的成功与否
19. this.$slots.default 是一个vnode 所以用于render而非template
20. setup有两个参数,第一个是props选项声明过的参数.第二个是ctx 包含{attrs(未声明props),emit,slots,expose}
21. 似乎只支持 onSubmit 小驼峰写法了监听事件
22. vue3ref  通过 ref() 生成的变量绑定在模板或者渲染函数中的ref 然后在onMounted 生命周期即可获得组件实例的cpn.value的Proxy 对象 ,而setup中的参数 expose 可以将ref获取到的实例对象改为expose暴露出的对象
23. computed 返回也是一个引用实现实例对象,且computed,和watch只能捕获到响应式数据的变化
24. watch 监听多个可以多次调用或者传入数组,接收到的新值旧值也是数组
25. - 引用数据类型新旧值相同的地址(vue2就有这个问题),
    - 似乎不需要deep:true就可以深度监听,(proxy对象不需要强制deep 函数返回对象需要deep,函数返回基本数据类型不需要多深都不需要
    - 无法监听对象的key这样监听.state.count 采用回调函数()=>state.count 
    - 无法监听到ref 中的proxy中的改变.需要通过.value直接监听proxy,或者开启deep
26. Vue3生命周期 app相对于vm更轻量化, unmounted,beforeUnmount重命名,必须挂载才能执行初始化init,(vue2可以再执行完created之后再挂载)
27. hooks 文件夹  useXXX.js
28. 直接return 响应式对象 或者return{...toRefs(响应式对象)},对象解构打断响应式是proxy的锅
29. 直接ref生成refImp 打断了关联,生成新的ref
30. shallowReactive 第一层响应式,内部怎么实现的??? (proxy 本身多层次的set就不会触发set,而是触发get
31. )shallowRef 不处理对象,即内部不调用reactive,第一层替换,或者为基本类型还是有响应式



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

  - 当 `ref` 作为响应式对象reactive的 property 被访问或更改时自动展开为value

  - 即访问state.ref = ref.value  访问 state[0] = ref

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

    执行时机,在setup函数相当于执行了一次函数,也可以在生命周期例如onMounted执行

    函数内的依赖值发生变化时重新执行

    ```
    const count = ref(0)
    watchEffect(() => count.value               // 函数的任何数据发生改变都会变化
    // -> logs 0								// 但是要具体到变化的值被引用才行
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

    - 依赖改变时重新执行的时机,缓冲同一队列的tick.,默认情况下 第三个参数 { flush: 'pre' } watchEffect的执行时机在onBeforeUpdate之前,可传入post,则在组件更新**后**重新运行侦听器副作用

    - > 我们之所以是通过传入一个函数去注册失效回调，而不是从回调返回它，是因为返回值对于异步错误处理很重要。
      >
      > 在执行数据请求时，副作用函数往往是一个异步函数：
      >
      > 应该是指watchEffect(()=>return 而不是从回调返回他,是因为返回值对于异步错误处理很重要。)

  - onInvalidate 清除时机

    - 副作用即将重新执行时(),先执行上一个watchEffect 的onInvalidate ,再执行新的onInvalidate 
    - stop()之后执行
    - 组件卸载后执行,自杀api已移除

- !! 这里有一个概念,执行了watchEffect函数,注册了传入watchEffect的回调函数,并执行一次,同理第一次进来要先执行onInvalidate函数并且注册onInvalidate里的回调.所以第一次注册 onInvalidate 里应当在所有watchEffect中的异步操作之前,否则异步操作会导致onInvalidate无法被注册

     ```
     const data = ref(null)
     watchEffect(async onInvalidate => {
       onInvalidate(() => {...}) // 我们在Promise解析之前注册清除函数
       data.value = await fetchData(props.id)
     })
     // 但还是有弊病,如果异步之后注册,那么第一次注册之前的change,onInvalidate无法清除,然后无论是在前还是在后,上一个await 还未来得及获取await 的token,就执行token.cancel,将会导致错误
     ```

     目前理解最好的解决方案,await 前后 loading, 最上方注册,onInvalidate清除结果注意null,还是会有突然强制销毁的可能

- 侦听器调试

  - `onTrack` 和 `onTrigger` 选项可用于调试侦听器的行为。`onTrack` 和 `onTrigger` 只能在开发模式下工作
  - `onTrack` 将在响应式 property 或 ref 作为依赖项被追踪时被调用。

  - `onTrigger` 将在依赖项变更导致副作用被触发时被调用。
  - 执行顺序watchEffect->onTrack->onTrigger->onInvalidate 

- `watch` 与 [`watchEffect`](https://vue3js.cn/docs/zh/guide/reactivity-computed-watchers.html#watcheffect)共享[停止侦听](https://vue3js.cn/docs/zh/guide/reactivity-computed-watchers.html#停止侦听)，[清除副作用](https://vue3js.cn/docs/zh/guide/reactivity-computed-watchers.html#清除副作用) (相应地 `onInvalidate` 会作为回调的第三个参数传入)、[副作用刷新时机](https://vue3js.cn/docs/zh/guide/reactivity-computed-watchers.html#副作用刷新时机)和[侦听器调试](https://vue3js.cn/docs/zh/guide/reactivity-computed-watchers.html#侦听器调试)行为。

  stop,onInvalidate, { flush: 'pre' },onTrack/onTrigger

- 组合式Api

  - 目前的复用仅仅是组件的复用,碎片化使得理解和复杂的组件变得困难,选项的分离掩盖了潜在的逻辑问题,在实际开发中,我经常需要通过ctrl+d去找到对应的逻辑,不断的跳转相关代码的选项块,虽然我自认为很酷,但在无注释的情况下,一段时间后会变得难以理解
  - setup在beforeCreated 之前执行,props 解析之后
  - ref 因为基本数据类型的传递是值传递,很不安全,容易在某个地方的时候失去他的响应式
  - 生命周期注册函数时,相同的函数只注册一次,可注册多个同名生命周期函数按顺序执行
  - proxy 空对象或者空数组 reactive({}) reactive([]) 整个替换的响应式 vue是无法捕捉的
  
- 生命周期函数

     - renderTracked  初次渲染追踪  传入event参数
     - renderTriggered  渲染触发更新  传入event参数 ,有new old value值
     - onErrorCaptured 捕获一个来自子孙组件的错误时被调用

- provide/inject

     ```
      provide: {
         todoLength: this.todos.length // 将会导致错误 'Cannot read property 'length' of undefined`
       },
       对象形式常量参数
      provide() {
         return {
           todoLength: this.todos.length
         }
       },
       函数使用this
       
     注入的如果是一个常量需要使用computed添加响应式(proxy对象不需要)
     
       provide() {
         return {
           todoLength: Vue.computed(() => this.todos.length)
         }
       }
     ```

     组合式provide/inject

     ```
       provide('location', 'North Pole')  key -value
         provide('geolocation', {
           longitude: 90,
           latitude: 135
         })
         
     const userLocation = inject('location', 'The Universe')  // 第二个参数未可选的默认参数
     const userGeolocation = inject('geolocation')
     ```

     添加响应式 ref,或者reactive包裹,直接provide提供 提供什么拿到什么...

     改变也应该在提供者内做出修改, 提供一个方法改变即可

     readonly 和原proxy或者refImp 不是相同的引用

- 模板引用

     - 模板中的ref  直接return 一个ref对象 demo ref='demo' 此处为字符串形式

     - jsx 中为 ref = { ref} 变量形式, 没为什么记住就好了 

     - v-for   

          - ```
               let itemRefs = [];
                 const setItemRef = (el) => {
                  itemRefs.push(el);
                 };
               ref= {itemRefs}
               ref={setItemRef.bind(null, index)}  null 占位
               ```

- 渲染机制和优化

     - dom的刷新更新很廉价,但是用js接触和计算dom,找到所需dom的成本很高,先更新virtual dom,在进行diff算法
     
- ts

     - 要让 TypeScript 正确推断 Vue 组件选项中的类型，需要使用 `defineComponent` 全局方法定义组件：

- 新特性

     - background: v-bind(color);

     - v-for 中的Ref 数组

     - 异步组件

          - defineAsyncComponent  由于函数式组件被定义为纯函数，因此异步组件的定义需要通过将其包装在新的 `defineAsyncComponent` 助手方法中来显式地定义：
          - component` 选项现在被重命名为 `loader  高阶用法的component
          - 接收一个返回promise 的函数且loader 函数不再接收resolve,reject

     - attribute 强制行为 ???/ 看不懂

     - 自定义指令

          - 多了一些新钩子,旧钩子修改名称
          - 目前多根节点指令会被忽略，并且会抛出一个警告。

     - 自定义元素交互

          - Vue.config.ignoredElements = ['plastic-button'] 不检查元素是否注册 2.x

          - 3.x 此检查在模板编译期间执行,  使用生成步骤,vite或者webpack 配置

          - ```js
               使用动态模板编译 const app = Vue.createApp({})
               app.config.isCustomElement = tag => tag === 'plastic-button'
               ```

     - data选项

       - 必须要返回对象
       - mixin 合并时,现在会浅层次的合并,

     - 事件API

       - $on,$off,$once 方法已移除,不推荐使用$bus,推荐使用mitt

     - 过滤器filter

       - 局部移除

       - 全局的可以通过app.config.globalProperties.$filters 自定义方法

       - ```
         import { getCurrentInstance } from 'vue' internalInstance.appContext.config.globalProperties
         ```

     - 片段

       - 允许多个根组件但是要求开发者明确定义属性部分分布在哪里

     - 函数式组件

          - `functional` attribute 在 `<template>` 中移除
          - `listeners` 现在作为 `$attrs` 的一部分传递，可以将其删除

     - 全局API

          - 缺点 Vue.directive,Vue.component 类似的全局API容易污染其他测试用例,
          - 3.x 将Vue.config 移到app.config
          - ...主要是开发者注意

     - 全局API Treeshaking

          - ????

     - 内联模板Attribute

          - 移除

     - key Attribute

          - 2.x 建议在v-if等条件分支加key  3.x 会自动生成唯一key
          - 2.x template 不能设置key,key需要设置在内部的节点   3.x  key 应该设置在template 标签上

     - 按键修饰符

          - 不再支持使用数字 (即键码) 作为 `v-on` 修饰符
          - 不再支持 `config.keyCodes`

     - 在prop中的default函数中访问this

          - ```
               import { inject } from 'vue'
               
               export default {
                 props: {
                   theme: {
                     default (props) {
                       // `props` 是传递给组件的原始值。
                       // 在任何类型/默认强制转换之前
                       // 也可以使用 `inject` 来访问注入的 property
                       return inject('theme', 'default-theme')
                     }
                   }
                 }
               }
               ```

     - 渲染函数API

          - h现在作为全局导入而不是从render中接收

     - Slot 统一

          - 移除 `this.$scopedSlots`

     - 过渡的class名更改

          - 修改了一些名字

     - v-model

          - 用于自定义组件,既非input select等 值为 modelValue 事件为 update:modelValue 
          - .sync 移除
          - 可以用v-models

     - v-if 与 v-for 的优先级对比
       - 现在if优先了

     - v-bind 的合并行为
       - 2.x 是单独的会覆盖object
       - 3.x更改为后绑定的优先
     
     
