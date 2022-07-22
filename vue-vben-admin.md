# vue-vben-admin

## .husky

- husky capture git commit  and pre-commit exe lint-staged  lint 
- script.prepare exe after yarn or npm install

## .vscode

- vscode ide config

## .gitpod

- .gitpod init directives

## yarn

- autoclean 默认关闭.当`.yarnclean`文件存在于包中时，以下情况之后将启用自动清理功能。清理将被执行：
  - install 之后
  - add 之后
  - `yarn autoclean --force`运行

## pretty-quick

Runs [Prettier](https://prettier.io/) on your changed files.

## commitlint

check commit 

## conventional

 generate changelog

## engines

limit node version

## commitizen

git cz

## esno

ts playground

## vue-tsc

Vue 3 command line Type-Checking tool base on IDE plugin [Volar](https://github.com/johnsoncodehk/volar).

## Workflow

- yarnclean
- eslint
- prettier
- stylelint
- lint-staged
- pretty
- husky
- commitlint
- conventional
- commitizen

# dotenv

parse .env object

## inquirer

User command line interaction

- type：表示提问的类型，包括：`input`, `confirm`, `list`, `rawlist`, `expand`, `checkbox`, `password`, `editor`；
- name: 存储当前问题回答的变量；

## http-server

- --cors 通过 Access-Control-Allow-Origin 标头启用 CORS
- -- gzip  基于 DEFLATE 算法，它是 LZ77 和霍夫曼编码的组合  最流行的压缩算法,兼容性强
-  --brotli 变种的 LZ77 算法,更高的压缩率,除了 IE 和 Opera Mini 之外其余都支持
- -c-1 缓存时默认开启的,加上-c-1禁用缓存

## flow

```
export type IPerson = {
  name: string
  age: number
}
or
export interface IPerson {
  name: string
  age: number
}
then
import type { IPerson } from './types/index.t'
```

## nvm

- settings.txt

  ```
  arch: 64 
  proxy: none 
  node_mirror: http://npm.taobao.org/mirrors/node/ 
  npm_mirror: https://npm.taobao.org/mirrors/npm/
  ```

- cmd

  ```
  nvm list  // 你本机中所有的node的版本列表
  nvm install latest  // 安装最新版本
  nvm install 4.8.4  // 安装指定版本
  nvm use 10.8.0  // 当前使用版本
  ```

## ant design vue

- ```
  import {Button } from 'ant-design-vue'
  <Button />
  or
  global register
  app.user(Button)
  <a>
  ```

  

## less

lessc style.less style.css

**@import(reference)** 不会编译引入的任何样式,只能用于变量,继承等

- css定义变量和使用

  ```
  --header-bg-hover-color: #273352;
  var(--header-bg-hover-color);
  ```

- less定义变量和使用

  ```
  @header-dark-bg-hover-color: var(--header-bg-hover-color);
  color:@header-dark-bg-hover-color
  ```

- 嵌套使用变量

  ```
  @namespace: zone;
  @prefix-cls: '@{namespace}-cropper-image'; // remember
  
  .foo {
    color: @prefix-cls;   color:'zone-cropper-image'; 有引号
  }
  //if
   @prefix-cls: ~'@{namespace}-cropper-image'; // remember
   
   .foo {
    color: zone-cropper-image; 无引号
  }
  
  then
  .@{prefix-cls} {
     
  }
  ```


## AES

- iv就是初始化向量，初始化向量的值依密码算法而不同。最基本的要求是“唯一性”，也就是说同一把密钥不重复使用同一个初始化向量

## svg

```
dom 内 又有svg 集合
<svg id="icon-zone"></svg>

就可以z
<svg >
    <use xlink:href="#icon-zone" />
</svg>
```

## >>> 0

1 . 如果不能转换为`Number`，那就为`0`

2 . 如果为非整数，先转换为整数，参考公式`sign(n) ⋅ floor(abs(n))`

3 . 如果是正数，返回正数，如果是负数，返回负数 + 2的32次方

## #

- chalk cmd color print

- process.argv.splice(2) [node url,exe.* url, Extra parameters]

- process.exit() or exit(0)  success exit   exit(1)  error exit

- Object.entries {key:value} =>[key,value]

- 只有以 `VITE_ `开头的变量会被嵌入到客户端侧的包中，你可以项目代码中这样访问它们：

- 以 `VITE_GLOB_*` 开头的的变量，在打包的时候，会被加入[_app.config.js](https://jekip.github.io/docs/guide/settings.html#生产环境动态配置)配置文件当中.

- javascriptEnabled+vite-plugin-style-import 作用域生产环境按需加载

- 引入antd.less,ant.css 才会去访问主题 modifyVars.hack

- import.meta.env .env中的变量会自动放入其中

- .js?v=?? 针对浏览器避免缓存,本地找不到该文件

- vite.config.js 这一步add process.env再build之后执行的js文件时就丢失了

- **不** 建议忽略自定义导入类型的扩展名（例如：`.vue`），因为它会影响 IDE 和类型支持。

- vite-glob-import

  ```
  const modules = import.meta.glob('./dir/*.js')
  
  // vite 生成的代码
  const modules = {
    './dir/foo.js': () => import('./dir/foo.js'),
    './dir/bar.js': () => import('./dir/bar.js')
  }
  匹配到的文件默认是懒加载的，通过动态导入实现，并会在构建时分离为独立的 chunk。如果你倾向于直接引入所有的模块（例如依赖于这些模块中的副作用首先被应用），你可以使用 import.meta.globEager 代替：
  ```

- \>>> 0

  1 . 如果不能转换为`Number`，那就为`0`

  2 . 如果为非整数，先转换为整数，参考公式`sign(n) ⋅ floor(abs(n))`

  3 . 如果是正数，返回正数，如果是负数，返回负数 + 2的32次方
