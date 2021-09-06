# JSX

## Vue2

- 在render中渲染xml 对象为underfined

- JSX就是Javascript和XML结合的一种格式。React发明了JSX，利用HTML语法来创建虚拟DOM。当遇到<，JSX就当HTML解析，遇到{就当JavaScript解析.

- JavaScript 的完全编程的能力。这时你可以用**渲染函数**，它比模板更接近编译器。
- 就是渲染层,可直接用例如可选链

- Vue 有一个babel 插件支持JSX语法 

  ```
  mounted(){ 
  	const element = <h1>Hello World</h1>
  	element // ->VNODE 虚拟节点(virtual node)  “虚拟 DOM”是我们对由 Vue 组件树建立起来的整个 VNode 树的称呼。
  }
  ```

- vue.runtime.esm.js?2b0e:619 [Vue warn]: Failed to mount component: template or render function not defined. 二选一

- data对象会被注入成vnode

一、Content

- basice content 

  ```
  render() {
    return <p>hello</p>
  }
  ```

  

- dynamic content  

  ```
  render() {
    return <p>hello { this.message }</p>
  }
  ```

- when self-closing:

  ```
  render() {
    return <input />
  }
  ```

- with a component:

  ```
  import MyComponent from './my-component'
  
  export default {
    render() {
      return <MyComponent>hello</MyComponent>
    },
  }
  ```

二、Attributes/Props

- basic  Attributes/Props

  ```
  render() {
    return <input type="email" />
  }
  ```

- with a dynamic binding:

  ```
  render() {
    return <input
      type="email"
      placeholder={this.placeholderText}
    />
  }
  ```

- with the spread operator (object needs to be compatible with [Vue Data Object](https://vuejs.org/v2/guide/render-function.html#The-Data-Object-In-Depth)):

  ```javascript
  render() {
    const inputAttrs = {
      type: 'email',
      placeholder: 'Enter your email'
    }
  
    return <input {...{ attrs: inputAttrs }} />
      
    const attrs = {
      type: 'email',
      placeholder: 'Enter your email',
        [this.title]: 'Enter your email' // 自定义b
    }
     return <input {...attrs} />
  }
  ```
  
  

三、Slots

- $slots  用来访问被[插槽分发](https://cn.vuejs.org/v2/guide/components.html#通过插槽分发内容)的内容。每个[具名插槽](https://cn.vuejs.org/v2/guide/components-slots.html#具名插槽)有其相应的 property (例如：`v-slot:foo` 中的内容将会在 `vm.$slots.foo` 中被找到)。`default` 

-  `vm.$scopedSlots`  作用域插槽 

-   {this.$slots.default}  { this.$scopedSlots.default() }    default  or custom name  

- ```
  const render = this.$scopedSlots.default()
      if (!render) return
  ```

- named slots:

  ```
  render() {
    return (
      <MyComponent>
        <header slot="header">header</header>
        <footer slot="footer">footer</footer>
      </MyComponent>
    )
  }
  ```

  - 在render里写插槽 写了template就必须要写 slot="default"

- scoped slots:

  ```
  render() {
    const scopedSlots = {
      header: (payLoad) => <header>header {payLoad.name}</header>,
      footer: (payLoad) => <footer>footer {payLoad.age}</footer>
    }
  
    return <MyComponent scopedSlots={scopedSlots} />
  }
  ```

四、Directives

- basic

```
$_handleInput(e) {
    this.name = e.target.value
}
 return <input value={this.name} onInput={this.$_handleInput}></input>
```

> 经我测试,在新版脚手架`vue-cli4`中，已经默认集成了对`v-model`的支持，大家可以直接使用``，如果你的项目比较老，也可以安装插件`babel-plugin-jsx-v-model`来进行支持

```
<input vModel={this.newTodoText} />
<input v-model={this.newTodoText} />
```

- with a modifier:

```
<input vModel_trim={this.newTodoText} />
```

- v-on

```
<input vOn:click={this.onClick} />
<input v-on:click={this.onClick} />
<input onClick={this.onClick} />
<input on-click={this.onClick} />
自定义event name
this.$emit('icon-click')
<input onIconClick={this.onClick} />
<input on={{'icon-click':this.onClick}} />
native修饰符
<input nativeOnClick={this.onClick} />
传参
<input on-click={this.onClick.bind(this,argument)} />
自定义事件名
on={{[this.event]:this.onClick}}

on-click={$event => this.event(param, $event)}
on-click={() => (this.???=???)}  e会自动传入作为最后一个参数
onClick={[onClick1,onClick2]}
```

- v-html:

```
<p domPropsInnerHTML={html} />
```

- v-text:

```
<p domPropsInnerText={text} />
```

- v-show

```
vShow={true}
v-show={true}
```

- .sync

```
<My-Component value={this.value} on={{'update:value':this.onInput}}/>
```

- v-if 与 v-for
- 遍历不用{}包裹

```
 const thead = this.hideHeader ? null : (<thead>
      {
        this.weekDays.map(day => <th key={day}>{ day }</th>)
      }
    </thead>)
{thead}
```

- 事件修饰符

  - `.stop` ： 阻止事件冒泡，在`JSX`中使用`event.stopPropagation()`来代替

  - `.prevent`：阻止默认行为，在`JSX`中使用`event.preventDefault()` 来代替

  - `.self`：只当事件是从侦听器绑定的元素本身触发时才触发回调，使用下面的条件判断进行代替

    ```
    if (event.target !== event.currentTarget){
    return
    }
    ```

  - `.enter`与`keyCode`: 在特定键触发时才触发回调

    ```
    if(event.keyCode === 13) {
    // 执行逻辑
    }
    ```

  - .once`,`.capture`,`.passive`,`.capture.once

    ```
      render() {
         return (
           <div
             on={{
             .capture 在冒泡排序中先捕获
             默认有里向外冒泡 有.captrue 优先 全部都有.captrue 向下冒泡
         1. 冒泡是从里往外冒，捕获是从外往里捕。
         1. 当捕获存在时，先从外到里的捕获，剩下的从里到外的冒泡输出。
               // 相当于 :click.capture
               '!click': this.$_handleClick,
               // 相当于 :input.once
               '~input': this.$_handleInput,
               // 相当于 :mousedown.passive
               '&mousedown': this.$_handleMouseDown,
               // 相当于 :mouseup.capture.once
               '~!mouseup': this.$_handleMouseUp
             }}
           ></div>
         )
       }
    ```
    

## Vue3

一 、 vite config

```
// vite.config.js
import vueJsx from '@vitejs/plugin-vue-jsx'

export default {
  plugins: [
    vueJsx({
      // options are passed on to @vue/babel-plugin-jsx
    })
  ]
}
```



二、Slots

**`v-slots`** 代替 *`scoped `*

slots.default?.()

```
<A>
    {{
        default: () => <div>A</div>,
        bar: () => <span>B</span>,
    }}
</A>
直接写在
```

