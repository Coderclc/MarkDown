# Vue_Study_Note

[toc]

## 一、VueCLI项目使用CDN优化

1. 在public/index.html引入CDN

## 二、对Vue不同构建版本的解释

完整版:包含完整的警告和调试模式和模板编译器(用来将模板字符串编译为js渲染函数的代码)

运行时版:删除了编译器

完整版(生产环境):删除了警告

运行时版(生产环境) 删除了警告和编译器

AMD和CMD模块以浏览器第一的原则发展，异步加载模块

CommonJS模块以服务器第一原则发展，选择同步加载 require() module. Exports= {} Node.js采用了这个规范。

UMD = AMD||CommonJS UMD为其糅合,优先判断支持AMD则使用

 ES Module  import _ from '' export

## 三、事件总线

轻量vuex $bus

Vue.prototype.$bus= new Vue() this.$bus.$emit("imgLoaded")this.$bus.$on("imgLoaded",()=>{console.log("我监听到了你的变化");})

 this.$bus.$off("imgLoaded",函数变量名)

## 四、Router-Link

\<router-link> 内部注册的组件  默认渲染为a标签  tag="button"  布尔属性 replace  不能返回

被选中的router-link 会自动添加类名 router-link-active,,可以通过属性active-class="active"修改生成的类名 也可以通过创建router instance option linkActiveClass:"active "

## 五、组件内的嵌套sync

子改变父必须update否则报错

所以如果一个变量绑定了子和孙,孙改变子,没问题,但此时子的改变若是父传递又会因为上面的原因导致报错,必须转载

```
  watch: {
    outerVisible(_) {
      this.outer = _
    },
    outer(_) {
      this.$emit('update:outerVisible', _)
    }
  }
  outerVisible为父子之间的通信  outer 为 子孙之间的通信
```



