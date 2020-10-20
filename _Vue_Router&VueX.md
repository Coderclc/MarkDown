# Vue_Router

[toc]

## 基础

tag切换

```html
<script src="https://unpkg.com/vue/dist/vue.js"></script>
<script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>
<router-link to="/foo">Go to Foo</router-link>
<router-link to="/bar">Go to Bar</router-link>
// 显示处
<router-view></router-view>

```

js切换

```
const router = new VueRouter({
  routes 
})
const app = new Vue({
  router
}).$mount('#app')
```

`this.$router` 访问路由器，也可以通过 `this.$route` 访问当前路由：

动态路由匹配

```
<router-link :to="{name/path: 'About', params: { id: 1 }}">About</router-link>

  {
    path: '/about:id',
    name: 'About',
    component: () => import(/* webpackChunkName: "about" */ '../views/About.vue')
  }
name对应params   path对应query
name对应的routes路径要加:,不加也能接受的到,但刷新即消失
```

 响应路由参数的变化 例如从 `/user/foo` 导航到 `/user/bar`，**原来的组件实例会被复用**。因为两个路由都渲染同个组件，比起销毁再创建，复用则显得更加高效。**不过，这也意味着组件的生命周期钩子不会再被调用**。

```
  watch: {
    $route(to, from) {
      // 对路由变化作出响应...
    }
  } 
  可通过哦watch监听,当然组件不能被销毁
```

捕获所有404或者NOTFOUND路由

 // 404 page must be placed at the end !!!

 { path: '*', redirect: '/404', hidden: true } 

```js
// 给出一个路由 { path: '/user-*' }
this.$router.push('/user-admin')
this.$route.params.pathMatch // 'admin'
```

嵌套路由即 <router-view>下有<router-view>

```
const router = new VueRouter({
  routes: [
    { path: '/user/:id', component: User,
      children: [
        {
          // 当 /user/:id/profile 匹配成功，
          // UserProfile 会被渲染在 User 的 <router-view> 中
          path: 'profile',
          component: UserProfile
        },
        {
          // 当 /user/:id/posts 匹配成功
          // UserPosts 会被渲染在 User 的 <router-view> 中
          path: 'posts',
          component: UserPosts
        }
      ]
    }
  ]
})
```

编程式的导航

router.push(location, onComplete?, onAbort?)

```
// 字符串
router.push('home')

// 对象
router.push({ path: 'home' })

// 命名的路由
router.push({ name: 'user', params: { userId: '123' }})

// 带查询参数，变成 /register?plan=private
router.push({ path: 'register', query: { plan: 'private' }})
```

```
const userId = '123'
router.push({ name: 'user', params: { userId }}) // -> /user/123
router.push({ path: `/user/${userId}` }) // -> /user/123
// 这里的 params 不生效
router.push({ path: '/user', params: { userId }}) // -> /user
```

router.replace(location, onComplete?, onAbort?) 相同的,但他不会往浏览器history添加记录

router.go(n) 前进回退history

命名路由,即路由选项的name属性,可用于切换

命名视图,即一个路径下有三个router-view,分别给他们命名

```
<router-view class="view one"></router-view>
<router-view class="view two" name="a"></router-view>
<router-view class="view three" name="b"></router-view>
 {
      path: '/',
      components: {  // 带s
        default: Foo,
        a: Bar,
        b: Baz
      }
    }
```

重定向和别名,即访问路径切换路径

```
const router = new VueRouter({
  routes: [
    { path: '/a', redirect: '/b' }
  ]
})
```

重定向的目标也可以是命名路由

```
const router = new VueRouter({
  routes: [
    { path: '/a', redirect: { name: 'foo' }}
  ]
})
```

注意[导航守卫](https://router.vuejs.org/zh/guide/advanced/navigation-guards.html)并没有应用在跳转路由上，而仅仅应用在其目标上。在下面这个例子中，为 `/a` 路由添加一个 `beforeEnter` 守卫并不会有任何效果。当他跳离不会有效果

别名即两个名字都能访问这个组件

```js
const router = new VueRouter({
  routes: [
    { path: '/a', component: A, alias: '/b' }
  ]
})
```

```
    children: [{
      path: '/(.*)/son1',
      component: () => import('@/components/Son1')
    },
    {
      path: '/(.*)/son2',
      component: () => import('@/components/Son2')
    }]
    // 匹配路径可用小括号的正则表达式
```

路由组件传参,params传递的参数,可通过设置路由属性



```
  {
    path: '/son1',
    name: 'Son1',
    component: () => import('@/components/Son1'),
    props: true
  } 
```

props:['id'] 即可在子组件中获取.减少使用$route耦合

```
  // 对于包含命名视图的路由，你必须分别为每个命名视图添加 `props` 选项：
    {
      path: '/user/:id',
      components: { default: User, sidebar: Sidebar },
      props: { default: true, sidebar: false }
    }
```

如果 `props` 被设置为 `true`，`route.params` 将会被设置为组件属性。

如果 `props` 是一个对象，它会被按原样设置为组件属性。当 `props` 是静态的时候有用。

```
const router = new VueRouter({
  routes: [
    { path: '/promotion/from-newsletter', component: Promotion, props: { newsletterPopup: false } }
  ]
}) 即传 newsletterPopup:false 到子组件
```

你可以创建一个函数返回 `props`。这样你便可以将参数转换成另一种类型，将静态值与基于路由的值结合等等。

```
    props: (route) => {
      return { hahahaha: route.params.id }
    }
    会把hahahaha作为key,值返回,并且可以操作,可以为params/query,但在这里操作不太好吧
```

html5的history模式  mode: 'history'

不过这种模式要玩好，还需要后台配置支持。因为我们的应用是个单页客户端应用，如果后台没有正确的配置，当用户在浏览器直接访问 `http://oursite.com/user/id` 就会返回 404，这就不好看了。

所以呢，你要在服务端增加一个覆盖所有情况的候选资源：如果 URL 匹配不到任何静态资源，则应该返回同一个 `index.html` 页面，这个页面就是你 app 依赖的页面。即设置nginx 404

```nginx
location / {
  try_files $uri $uri/ /index.html;
}
```

给个警告，因为这么做以后，你的服务器就不再返回 404 错误页面，因为对于所有路径都会返回 `index.html` 文件。为了避免这种情况，你应该在 Vue 应用里面覆盖所有的路由情况，然后在给出一个 404 页面。

```js
const router = new VueRouter({
  mode: 'history',
  routes: [
    { path: '*', component: 404 }
  ]
})
```

## 进阶

当一个导航触发时，全局前置守卫按照创建顺序调用。守卫是异步解析执行，此时导航在所有守卫 resolve 完之前一直处于 **等待中**。

每个守卫方法接收三个参数：

- **`to: Route`**: 即将要进入的目标 [路由对象](https://router.vuejs.org/zh/api/#路由对象)
- **`from: Route`**: 当前导航正要离开的路由
- **`next: Function`**: 一定要调用该方法来 **resolve** 这个钩子。执行效果依赖 `next` 方法的调用参数。
  - **`next()`**: 进行管道中的下一个钩子。如果全部钩子执行完了，则导航的状态就是 **confirmed** (确认的)。
  - **`next(false)`**: 中断当前的导航。如果浏览器的 URL 改变了 (可能是用户手动或者浏览器后退按钮)，那么 URL 地址会重置到 `from` 路由对应的地址。
  - **`next('/')` 或者 `next({ path: '/' })`**: 跳转到一个不同的地址。当前的导航被中断，然后进行一个新的导航。你可以向 `next` 传递任意位置对象，且允许设置诸如 `replace: true`、`name: 'home'` 之类的选项以及任何用在 [`router-link` 的 `to` prop](https://router.vuejs.org/zh/api/#to) 或 [`router.push`](https://router.vuejs.org/zh/api/#router-push) 中的选项。
  - **`next(error)`**: (2.4.0+) 如果传入 `next` 的参数是一个 `Error` 实例，则导航会被终止且该错误会被传递给 [`router.onError()`](https://router.vuejs.org/zh/api/#router-onerror) 注册过的回调。

全局前置守卫 router.beforeEach((to, from, next) 

全局解析守卫 router.beforeResolve**同时在所有组件内守卫和异步路由组件被解析之后**，解析守卫就被调用

全局后置router.afterEach((to, from)

路由独享 写在路由上

```
const router = new VueRouter({
  routes: [
    {
      path: '/foo',
      component: Foo,
      beforeEnter: (to, from, next) => {
        // ...
      }
    }
  ]
})
```

组件内守卫

- `beforeRouteEnter`
- `beforeRouteUpdate` (2.2 新增)
- `beforeRouteLeave`

```
const Foo = {
  template: `...`,
  beforeRouteEnter (to, from, next) {
    // 在渲染该组件的对应路由被 confirm 前调用
    // 不！能！获取组件实例 `this`
    // 因为当守卫执行前，组件实例还没被创建
  },
  beforeRouteEnter (to, from, next) {
  next(vm => {
    // 通过 `vm` 访问组件实例  可以在这里访问实例
  })
}
  beforeRouteUpdate (to, from, next) {
    // 在当前路由改变，但是该组件被复用时调用
    // 举例来说，对于一个带有动态参数的路径 /foo/:id，在 /foo/1 和 /foo/2 之间跳转的时候，
    // 由于会渲染同样的 Foo 组件，因此组件实例会被复用。而这个钩子就会在这个情况下被调用。
    // 可以访问组件实例 `this`
    不支持传递回调
  },
  beforeRouteLeave (to, from, next) {
    // 导航离开该组件的对应路由时调用
    // 可以访问组件实例 `this`
    不支持传递回调
  }
}
```

路由元信息 meta  meta: { requiresAuth: true } 在 $route.matched访问  to.matched

过渡动效,即transiton包裹routerview,发挥你的创造力

给路由设置不同的过渡效果,设置name

```
const Foo = {
  template: `
    <transition name="slide">
      <div class="foo">...</div>
    </transition>
  `
}

const Bar = {
  template: `
    <transition name="fade">
      <div class="bar">...</div>
    </transition>
  `
}
```

根据路由动态过渡效果

```
<!-- 使用动态的 transition name -->
<transition :name="transitionName">
  <router-view></router-view>
</transition>
// 接着在父组件内
// watch $route 决定使用哪种过渡
watch: {
  '$route' (to, from) {
    const toDepth = to.path.split('/').length
    const fromDepth = from.path.split('/').length
    this.transitionName = toDepth < fromDepth ? 'slide-right' : 'slide-left'
  }
}
```

数据获取有两种情况

**导航完成之后获取**：先完成导航，然后在接下来的组件生命周期钩子中获取数据。在数据获取期间显示“加载中”之类的指示。

**导航完成之前获取**：导航完成前，在路由进入的守卫中获取数据，在数据获取成功后执行导航。

```
  watch: {
    // 当监听到如果路由有变化，会再次执行该方法
    '$route': 'fetchData'
  },
  
```

滚动行为,切换路由时,希望页面滚动的位置

```
const router = new VueRouter({
  routes: [...],
  scrollBehavior (to, from, savedPosition) {
    // return 期望滚动到哪个的位置
  }
})
 scrollBehavior: () => ({ y: 0 }),
```

```
滚动到锚点
scrollBehavior (to, from, savedPosition) {
  if (to.hash) {
    return {
      selector: to.hash
    }
  }
}
```

# VueX

## 介绍

全局状态管理模式,集成devtools

组件内的状态管理模式    view actions state 循环

vuex管理模式	

![image-20201018230706250](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201018230706250.png)

如果同步操作可跳过actions

每一个 Vuex 应用的核心就是 store（仓库）。“store”基本上就是一个容器，它包含着你的应用中大部分的**状态 (state)**。

(改的话能改)你不能直接改变 store 中的状态。改变 store 中的状态的唯一途径就是显式地**提交 (commit) mutation**。这样使得我们可以方便地跟踪每一个状态的变化，从而让我们能够实现一些工具帮助我们更好地了解我们的应用。

通过 `store.state` 来获取状态对象 通过 store.commit('increment')触发

## 核心概念

state 为一个对象,

getter中函数有两个参数 state,getter

mutation中函数有两个参数 state ,payload

action函数有一个参数 context:{commit,dispatch 等..}

### state

store中的state使用computed计算属性返回  count : return this.$store.state.count

mapState函数   返回一个对象, 使用展开运算符 ... 与本地计算属性合并

```
/ 在单独构建的版本中辅助函数为 Vuex.mapState
import { mapState } from 'vuex'

export default {
  data(){return{localCount:12}},
  computed: mapState({
    // 箭头函数可使代码更简练
    count: state => state.count,

    // 传字符串参数 'count' 等同于 `state => state.count`
    countAlias: 'count',

    // 为了能够使用 `this` 获取局部状态，必须使用常规函数
    countPlusLocalState (state) {
      return state.count + this.localCount
    }
  })
}
// 也可以直接
computed: mapState([
  // 映射 this.count 为 store.state.count
  'count'
])
```

### Getters

 this.$store.getters.ccount 访问

```
getters: {
  // ...
  doneTodosCount: (state, getters) => {  // 接受两个参数
    return getters.doneTodos.length
  }
}
```

同理`mapGetters`

```
computed:mapGetters([
      'doneTodosCount',
      'anotherGetter',
      // ...
    ])
  ...mapGetters({
  // 把 `this.doneCount` 映射为 `this.$store.getters.doneTodosCount`
  doneCount: 'doneTodosCount'
})
对象形式改名字
```

### Mutation

```
const store = new Vuex.Store({
  state: {
    count: 1
  },
  mutations: {
    increment (state,payload) {
      // 变更状态
      state.count++
    }
  }
})
store.commit('increment',payload) 提交载荷payload
大多数情况下载荷应该是个对象
```

```
还可以采用这种提交风格,当上面的载荷是一个对象,与这种风格对应的mutation code 一样
store.commit({
  type: 'increment',
  amount: 10
})
mutation 中不变
```

Mutation需遵守Vue的相应规则,最好是在store中先定义好初始值,如果你希望后面添加新的store.state属性

当需要在对象上添加新属性时，你应该  Vue.set(obj, 'newProp', 123) 

或者state.obj = { ...state.obj, newProp: 123 }

使用常量代替mutation事件类型

```
// mutation-types.js  命名规范
export const SOME_MUTATION = 'SOME_MUTATION'
// store.js
import Vuex from 'vuex'
import { SOME_MUTATION } from './mutation-types'
const store = new Vuex.Store({
  state: { ... },
  mutations: {
    // 我们可以使用 ES2015 风格的计算属性命名功能来使用一个常量作为函数名
    [SOME_MUTATION] (state) {
      // mutate state
    }
  }
})
```

mapMutations

```
import { mapMutations } from 'vuex'

export default {
  // ...
  methods: {
    ...mapMutations([
      'increment', // 将 `this.increment()` 映射为 `this.$store.commit('increment')`
      // `mapMutations` 也支持载荷：
      'incrementBy' // 将 `this.incrementBy(amount)` 映射为 `this.$store.commit('incrementBy', amount)`
    ]),
    ...mapMutations({
      add: 'increment' // 将 `this.add()` 映射为 `this.$store.commit('increment')`
    })
  }
}
```

### Actions

```
 // dispatch
 increment() {
      this.$store.dispatch('INCREMENTASYNC', { num: 233 })
 }
  actions: { // 传的是context
    INCREMENTASYNC(context:{ store, commit }, payload) {  // 可以直接解构commit
      setTimeout(() => {
        commit('INCREMENT', payload)
      }, 2000)
    }
  }
 
```

Action 函数接受一个与 store 实例具有相同方法和属性的 context 对象，因此你可以调用 `context.commit` 提交一个 mutation，或者通过 `context.state` 和 `context.getters` 来获取 state 和 getters。当我们在之后介绍到 [Modules](https://vuex.vuejs.org/zh/guide/modules.html) 时，你就知道 context 对象为什么不是 store 实例本身了。

```
// 以载荷形式分发
store.dispatch('incrementAsync', {
  amount: 10
})

// 以对象形式分发
store.dispatch({
  type: 'incrementAsync',
  amount: 10
})
```

同理有两种方式分发 

mapActions函数

```
import { mapActions } from 'vuex'

export default {
  // ...
  methods: {
    ...mapActions([
      'increment', // 将 `this.increment()` 映射为 `this.$store.dispatch('increment')`

      // `mapActions` 也支持载荷：
      'incrementBy' // 将 `this.incrementBy(amount)` 映射为 `this.$store.dispatch('incrementBy', amount)`
    ]),
    ...mapActions({
      add: 'increment' // 将 `this.add()` 映射为 `this.$store.dispatch('increment')`
    })
  }
}
```

组合action即 action中的异步完成时,返回一个promise

```
actions: {
  actionA ({ commit }) {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        commit('someMutation')
        resolve()
      }, 1000)
    })
  }
}
```

```
// 组件中就可以捕捉,知道几时完成
store.dispatch('actionA').then(() => {
  // ...
})
```

```
// 派遣B,B中派遣A,A的结果之后commit ,并返回给派遣B的发生器
actions: {
  // ...
  actionB ({ dispatch, commit }) {
    return dispatch('actionA').then(() => {
      commit('someOtherMutation')
    })
  }
}
```

```

actions: {
  async actionA ({ commit }) {
    commit('gotData', await getData())
  },
  async actionB ({ dispatch, commit }) {
    await dispatch('actionA') // 等待 actionA 完成
    commit('gotOtherData', await getOtherData())
  }
}
// 组合拳
```

### Moudles

state:()=>({})

mutation state,payload

action 一个对象 context{ state, commit, rootState }

getter四个参数  (state, getters, rootState,rootgetter) 

$store.state.userModules.user 访问 state

```
const moduleA = {
  state: () => ({ ... }), // 注意格式  直接为一个对象也行
  mutations: { ... },
  actions: { ... },
  getters: { ... }
}
const store = new Vuex.Store({
  modules: {
    a: moduleA,
  }
})
store.state.a // -> moduleA 的状态

```

对于模块内部的 mutation 和 getter，接收的第一个参数是**模块的局部状态对象**。

```
const moduleA = {
  state: () => ({
    count: 0
  }),
  mutations: {
    increment (state) { // 模块的state
      // 这里的 `state` 对象是模块的局部状态
      state.count++
    }
  },

  getters: {  // 三个传入参数
    doubleCount (state,getters,rootState) {
      return state.count * 2
    }
  }
}
```

```
const moduleA = {
  // ...
  actions: { // 模块的 ,根节点的state   context:{}
    incrementIfOddOnRootSum ({ state, commit, rootState }) {
      if ((state.count + rootState.count) % 2 === 1) {
        commit('increment')
      }
    }
  }
}
```

命名空间默认情况下，模块内部的 action、mutation 和 getter 是注册在**全局命名空间**的——这样使得多个模块能够对同一 mutation 或 action 作出响应。

```
    userModules: {
      ...userModules,
      namespaced: true
    }
    commit 和dispatch 时需要加模块名称
    this.$store.commit('userModules/REDUCE')
          // 模块内容（module assets）
      state: () => ({ ... }), // 模块内的状态已经是嵌套的了，使用 `namespaced` 属性不会对其产生影响
      getters: {
        isAdmin () { ... } // -> getters['account/isAdmin']
      },
      actions: {
        login () { ... } // -> dispatch('account/login')
      },
      mutations: {
        login () { ... } // -> commit('account/login')
      },
```

在带命名空间的模块内访问全局内容（Global Assets）

```
modules: {
  foo: {
    namespaced: true,

    getters: {
      // 在这个模块的 getter 中，`getters` 被局部化了
      // 你可以使用 getter 的第四个参数来调用 `rootGetters`
      someGetter (state, getters, rootState, rootGetters) {
        getters.someOtherGetter // -> 'foo/someOtherGetter'
        rootGetters.someOtherGetter // -> 'someOtherGetter'
      },
      someOtherGetter: state => { ... }
    },

    actions: {
      // 在这个模块中， dispatch 和 commit 也被局部化了
      // 他们可以接受 `root` 属性以访问根 dispatch 或 commit
      someAction ({ dispatch, commit, getters, rootGetters }) {
        getters.someGetter // -> 'foo/someGetter'
        rootGetters.someGetter // -> 'someGetter'
	    
        dispatch('someOtherAction') // -> 'foo/someOtherAction'访问模块中的action
        dispatch('someOtherAction', null, { root: true }) // -> 'someOtherAction'

        commit('someMutation') // -> 'foo/someMutation'
        commit('someMutation', null, { root: true }) // -> 'someMutation'
      },
      someOtherAction (ctx, payload) { ... }
    }
  }
}
```

在命名模块中注册全局action 

若需要在带命名空间的模块注册全局 action，你可添加 `root: true`，并将这个 action 的定义放在函数 `handler` 中。例如：

```
{
  actions: {
    someOtherAction ({dispatch}) {
      dispatch('someAction')
    }
  },
  modules: {
    foo: {
      namespaced: true,

      actions: {
        someAction: {
          root: true,
          handler (namespacedContext, payload) { ... } // -> 'someAction'
        }
      }
    }
  }
}
```

命名空间的绑定函数

当使用 `mapState`, `mapGetters`, `mapActions` 和 `mapMutations` 这些函数来绑定带命名空间的模块时，写起来可能比较繁琐：

```

    this.$store.commit('userModules/someMutation')
    this['userModules/someMutation']()
```

对于这种情况，你可以将模块的空间名称字符串作为第一个参数传递给上述函数，这样所有绑定都会自动将该模块作为上下文。于是上面的例子可以简化为：

```

 ...mapMutations('userModules', ['someMutation'])
 this.someMutation()
```

而且，你可以通过使用 `createNamespacedHelpers` 创建基于某个命名空间辅助函数。它返回一个对象，对象里有新的绑定在给定命名空间值上的组件绑定辅助函数：

```

import { createNamespacedHelpers } from 'vuex'
const { mapMutations } = createNamespacedHelpers('userModules')  模块名
...mapMutations(['someMutation'])和全局一样使用
```

#### 给插件开发者的注意事项

如果你开发的[插件（Plugin）](https://vuex.vuejs.org/zh/guide/plugins.html)提供了模块并允许用户将其添加到 Vuex store，可能需要考虑模块的空间名称问题。对于这种情况，你可以通过插件的参数对象来允许用户指定空间名称：

```
// 通过插件的参数对象得到空间名称
// 然后返回 Vuex 插件函数
export function createPlugin (options = {}) {
  return function (store) {
    // 把空间名字添加到插件模块的类型（type）中去
    const namespace = options.namespace || ''
    store.dispatch(namespace + 'pluginAction')
  }
}
```



## 进阶

项目结构

