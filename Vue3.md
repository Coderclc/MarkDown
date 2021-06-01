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