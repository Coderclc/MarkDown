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

  - 将$listeners 移到了$attrs  ,使用 v-bind="$attrs" 也要把 inheritAttrs: false,带上

- 多个根节点, 现在可以是多个根节点了
  - 不具有自动 attribute 回退行为。如果未显式绑定 `$attrs`，将发出运行时警告。
- 在dom模板中@myEvent 无法接受到 emit('myEvent') 需为@my-event