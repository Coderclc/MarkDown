# Vue Style Guide

[toc]

## 优先级A:必要的

1. 组件名为多个单词,详细点比较好
2. prop声明越详细越好至少要指定类型
3. 避免v-if和v-for一起使用
4. 为子组件样式设置scoped  全局 App 导入基本样式.采用BEM(block-element_modifed)命名样式SCSS
5. 私有属性名为插件、混入等不考虑作为对外公共 API 的自定义私有 property 使用 `$_` 前缀。 $_updated__ 避免和作者冲突

## 优先级B:强烈推荐

1. 能用单文件就用单文件
2. 单文件命名采用PascalCase或者kebab-case, 默认index.vue小写
3. 基础组件名,给有关联的基础组件加特定前缀(\- BaseButton.vue |- BaseTable.vue |- BaseIcon.vue)
4. 单例组件名,即不接受props,可用于多个页面的单词 加The前缀 TheHeading.vue
5. 紧密耦合组件名.例如|- TodoList.vue |- TodoListItem.vue |- TodoListItemButton.vue
6. 组件名的命名.一般化描述开头,修饰结尾SearchInputQuery > SearchInput
7. 自闭合组件,在单文件无内容使用自闭合
8. 模板中组件名大小写,PascalCase或者kebab-case, 
9. 完整单词的组件名 名字单词长一点无所谓
10. prop和方法 声明的时候采用camelCase,使用的时候采用kebab-case
11. 多个attr的元素分行写
12. 能用methods或者computed就不要直接在mustache中写表达式
13. 复杂的计算属性可以拆成多个计算属性写

## 优先级C:推荐

1. 模板选项顺序

   ```
   副作用 (触发组件外的影响)
   
   el
   全局感知 (要求组件以外的知识)
   
   name
   parent
   组件类型 (更改组件的类型)
   
   functional
   模板修改器 (改变模板的编译方式)
   
   delimiters
   comments
   模板依赖 (模板内使用的资源)
   
   components
   directives
   filters
   组合 (向选项里合并 property)
   
   extends
   mixins
   接口 (组件的接口)
   
   inheritAttrs
   model
   props/propsData
   本地状态 (本地的响应式 property)
   
   data
   computed
   事件 (通过响应式事件触发的回调)
   
   watch
   生命周期钩子 (按照它们被调用的顺序)
   beforeCreate
   created
   beforeMount
   mounted
   beforeUpdate
   updated
   activated
   deactivated
   beforeDestroy
   destroyed
   非响应式的 property (不依赖响应系统的实例 property)
   
   methods
   渲染 (组件输出的声明式描述)
   
   template/render
   renderError
   ```

2. 元素attr顺序

   ```
   定义 (提供组件的选项)
   
   is
   列表渲染 (创建多个变化的相同元素)
   
   v-for
   条件渲染 (元素是否渲染/显示)
   
   v-if
   v-else-if
   v-else
   v-show
   v-cloak
   渲染方式 (改变元素的渲染方式)
   
   v-pre
   v-once
   全局感知 (需要超越组件的知识)
   
   id
   唯一的 attribute (需要唯一值的 attribute)
   
   ref
   key
   双向绑定 (把绑定和事件结合起来)
   
   v-model
   其它 attribute (所有普通的绑定或未绑定的 attribute)
   
   事件 (组件事件监听器)
   
   v-on
   内容 (覆写元素的内容)
   
   v-html
   v-text
   ```

3. 不要用元素选择器

4. 不要使用边界情况的this.$parent  this.$children

5. 能用vuex就用vuex

   

