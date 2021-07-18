# Vue3

## Change

1. monorepo 管理 
   - mono 单个,repo repository仓库
   - 多个包之间相互独立,有自己的功能逻辑,单元测试,同一个仓库下方便管理
   - 模块划分清晰,可维护性,可拓展性强
2. Vue3改用es6的Proxy实现劫持
   - Vue2.x使用的Object.defineProperty来劫持obj的getter和setter,缺陷是设置和删除无法劫持,所以用相应的hack方法api$delete,$set,
3. 删除了一些不必要的api
   - 删除了$on,$off,$once,
   - 移除了filter,内联模板(在父组件中声明的数据和子组件中声明的数据两个都可以渲染,这反而是缺点)等
4. 编译方面的优化
   - 生成block tree ,slot编译优化,diff算法优化
5. 由Options API到Composition Api
   - 在Vue2.x通过Options API来描述组件对象,包括 data,props,methods,computed,生命周期等选项,问题在于多个逻辑可能实在不同的地方,跳来跳去?
   - composition API 可以将相关联的代码放到同一行进行处理,而不需要在多个Options之间寻找
6. Hooks 函数增加代码的复用性
   - Vue2.x使用mixins来共享组件逻辑,缺陷在于mixins也使由Options组成的,多个mixins会存在命名冲突的问题,
   - 3.x可以通过hook函数,将一部分独立的逻辑抽取出去,并且还能做到是响应式的



# Vue3

```
<div id="app">
  {{ message }}
</div>

var app = new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue!'
  }
})
```

- 非.vue除了挂载方式 不同其余相同

```
<div id="counter">
  Counter: {{ counter }}
</div>

const Counter = {
  data() {
    return {
      counter: 0
    }
  }
}

Vue.createApp(Counter).mount('#counter')
```

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

- `v-for` 渲染的元素列表时，它默认使用“就地更新”的策略。不会移动dom 的顺序,而是就地更新,提供key attr即可.建议尽可能在使用 `v-for` 时提供 `key` attribute，除非遍历输出的 DOM 内容非常简单，或者是刻意依赖默认行为以获取性能上的提升。意思是提供了key反而会降低性能?

  > `key` 的特殊 attribute 主要用在 Vue 的虚拟 DOM 算法，在新旧 nodes 对比时辨识 VNodes。如果不使用 key，Vue 会使用一种最大限度减少动态元素并且尽可能的尝试就地修改/复用相同类型元素的算法。而使用 key 时，它会基于 key 的变化重新排列元素顺序，并且会移除/销毁 key 不存在的元素。

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

- v-once 用用于大量的静态html文本

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

  - 自定义选项合并策略
  - 在vue2中mixins有几个问题第一,mixin很容易发生冲突第二,可重用性是有限的,我们不能向mixin传递任何参数来改变他的逻辑 ->组合式api

- directive

  - 包含以下几个钩子函数beforeMount,mounted,beforeUpdate,updated,beforeUnmount,unmounted
  - 你可能想在 `mounted` 和 `updated` 时触发相同行为，而不关心其它的钩子。比如这样写：指令名后面直接加函数

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

  - 可选的第二个参数{Object} props却报错了

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

    
