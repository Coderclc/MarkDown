# Webpack

[toc]

## Issue

1. webpack.NamedModulesPlugin is not a constructor
2. sideEffects:false 导致css无法被打包
3. new webpack.BannerPlugin("版权归 clc 所有") 版權插件

## 安装

```
4.0 以下              webpack   ./src/index.js     ./dist/bundle.js    ->bundle.js
4.0 以上还需要webcli    webpack   ./src/index.js -o  ./dist              ->main.js
```

4.0 以上 install "webpack-cli": "^4.1.0"

通过script脚本默认运行node_modules本地寻找

```
"scripts": {
    "start": "webpack" 默认会去找 --config webpack.config.js
}
exe webpack by webpack.config.js
```

## 起步

并且移除 `main` 入口。这可以防止意外发布你的代码。 [npm](https://docs.npmjs.com/files/package.json)

\<script>标签管理项目的问题

1. 隐式依赖关系,无法立即体现，脚本的执行依赖于外部扩展库(external library)
2. 如果依赖不存在，或者引入顺序错误，应用程序将无法正常运行
3. 如果依赖被引入但是并没有使用，浏览器将被迫下载无用代码

`npx webpack`，会将我们的脚本作为[入口起点](https://www.webpackjs.com/concepts/entry-points)，然后 [输出](https://www.webpackjs.com/concepts/output) 为 `main.js`。Node 8.2+ 版本提供的 `npx` 命令，可以运行在初始安装的 webpack 包(package)的 webpack 二进制文件

*注意，当在 windows 中通过调用路径去调用* `webpack` *时，必须使用反斜线()。例如* `node_modules\.bin\webpack --config webpack.config.js`*。*

*通过向* `npm run build` *命令和你的参数之间添加两个中横线，可以将自定义参数传递给 webpack，例如：*`npm run build -- --colors`*。*

## 管理资源

动态打包所有的依赖项,通过 loader *引入任何其他类型的文件*。

```
{
    test: /\.(png|svg|jpeg|gif)$/,
    use: [{
        loader: 'file-loader',
        options: {
            outputPath: './img'
            // publicPath: './img'
        }
    }]
}
```

解析 :webpack	根据正则表达式匹配决定哪些文件使用那些loader

 默认情况 css code 会被注入到madin.js文件中 ,多数情况进行css分离(使用extract-text-webpack-plugin插件)有利于生产环境加载速度提升

use: [ 'style-loader', 'css-loader' ]顺序很重要,加载顺序为从右到做

1. 加载Css  [style-loader](https://www.webpackjs.com/loaders/style-loader) (将css-loader内部样式注入到我们的HTML页面)和 [css-loader](https://www.webpackjs.com/loaders/css-loader)(加载.css文件)：

2. file-loader,加载图片,字体并转存到dist文件夹下

3. 当文件较小时可使用`url-loader` 功能类似于 [`file-loader`](https://github.com/webpack-contrib/file-loader)，但是在文件大小（单位 byte）低于指定的限制时，可以返回一个 DataURL。

4. 加载数据如JSON 文件，CSV、TSV 和 XML使用[csv-loader](https://github.com/theplatapi/csv-loader) 和 [xml-loader](https://github.com/gisikw/xml-loader)。让我们处理这三类文件：

   在 webpack 出现之前，前端开发人员会使用 grunt 和 gulp 等工具来处理资源
   
5.  url loader limit: 当图片的大小 kb*1024 小于 limit 会将图片编译成 bae64 字符串形式直接保存在 文件中. 大于使用 file loader,会把图片打包到 dist 

## 管理输出

一旦开始对文件名使用哈希hash并输出多个bundle时,此时需要手动给index.html挂载多个bundle,一切就变得困难起来.

使用HtmlWebpackPlugin管理输出 HtmlWebpackPlugin会默认生成 `index.html` 文件。这就是说，它会用新生成的 `index.html` 文件，把我们的原来的替换。新的index.html导入了所有bundle.js

使用clean-webpack-plugin在每次打包之前清理dist文件夹 const { CleanWebpackPlugin } = require('clean-webpack-plugin')

使用HtmlWebpackPlugin html可自动关联打包好的js文件

使用[`clean-webpack-plugin`](https://www.npmjs.com/package/clean-webpack-plugin)清理文件夹

webpack及其插件似乎“知道”应该哪些文件生成。答案是，通过 manifest

## 开发

source map  源文件会打包整合到一个bundle.js,此时很难追踪错误和警告来自于哪个源文件

选择一个watch开发工具

1. webpack's Watch Mode  "watch": "webpack --watch",  检测到代码修改就重新打包
2. webpack-dev-server webpack-cli@3
3. webpack-dev-middleware

webpack server 只需配置

```
 devServer: {
+     contentBase: './dist'
+   }
```

以上配置告知 `webpack-dev-server`，在 `localhost:8080` 下建立服务，将 `dist` 目录下的文件，作为可访问文件。

 webpack-dev-server 帮我们打包生成的 bundle.js 文件，并没有放到 实际的 物理磁盘上；而是直接托管到了 电脑的内存中，所以，我们在 项目根目录中，根本找不到 这个打包好的 bundle.js；

`webpack-dev-middleware` 是一个容器(wrapper)，它可以把 webpack 处理后的文件传递给一个服务器(server)。 `webpack-dev-server` 在内部使用了它，同时，它也可以作为一个单独的包来使用，以便进行更多自定义设置来实现更多的需求。结合server,koa,

```
const config = require('./webpack.config.js')
const compiler = webpack(config) 生成编译器
```

--inline 默认开启,浏览器刷新应用程序启用*内联模式(inline mode)*。一段处理实时重载的脚本被插入到你的包(bundle)中并且构建消息将会出现在浏览器控制台。

```
log.js?4244:23 [HMR] Waiting for update signal from WDS...
```

*荐使用模块热替换的内联模式，因为它包含来自 websocket 的 HMR 触发器。轮询模式可以作为替代方案，但需要一个额外的入口点：*`'webpack/hot/poll?1000` 

--process 将运行进度输送到控制台

## 模块热替换

HMR Hot Module Replacement 它允许在运行时更新各种模块，而无需进行完全刷新

**永远不要***在生产环境(production)下启用 HMR* 引入的插件会使bundle很大

即默认情况当webpack-dev-server监测到code变换时,会进行刷新,并且重置浏览器,但如果需要触发事件添加样式。那么每一次刷新就会使之前触发事件后的样式消失，需要重新触发样式。{hot:true //开启hmr,hotOnly:true //即使不生效也不刷新浏览器}.*HMR只支持样式文件，不适用于js等文件。*

当同时使用 webpack dev server 和 Node.js API 时，不要将 dev server 选项放在 webpack 配置对象中。而是，在创建选项时，将其作为第二个参数传递。即结webpack-dev-server和webpack-dev-middleware结合server使用时

js文件的模块热替换需要使用 module.hot.accept监听,并修改.csshmr就很容易 ,loader在后台会`module.hot.accept` 来修补(patch) `<style>` 标签。

## Tree shaking

*ree shaking* 是一个术语，通常用于描述移除 JavaScript 上下文中的未引用代码(dead-code)。

webpack5+默认打包是采用production环境,默认treeshaking, 如果采用--mode = development,则会将dead-code也打包到bundle中

新的 webpack 4 正式版本，扩展了这个检测能力，通过 `package.json` 的 `"sideEffects"` 属性作为标记，向 compiler 提供提示，表明项目中的哪些文件是 "pure(纯的 ES2015 模块)"，由此可以安全地删除文件中未使用的部分。

在package.json 设置字段sideEffects为false,webpack就会放心的把未使用的export删除作用同 `babel-plugin-import`

*「副作用」的定义是，在导入时会执行特殊行为的代码，而不是仅仅暴露一个 export 或多个 export。举例说明，例如 polyfill，它影响全局作用域，并且通常不提供 export。*部分代码字段有副作用,sideEffects可以设置为数组

压缩输出,既*UglifyJSPlugin*设置mde导出mode,或者webpack --mode production

## 生产环境构建

开发环境:我们需要具有强大的、具有实时重新加载(live reloading)或热模块替换(hot module replacement)能力的 source map 和 localhost server。

生产环境:更小的 bundle，更轻量的 source map，以及更优化的资源，以改善加载时间。由于要遵循逻辑分离

遵循不重复原则DRY don'trepeatyourself,将通用配置提取,使用`webpack-merge`合并

webpack.base.conf.js webpack.dev.conf.js webpack.prod.conf.js

好用的Minification插件**[babel-minify-webpack-plugin](https://github.com/webpack-contrib/babel-minify-webpack-plugin)**和**[webpack-closure-compiler](https://github.com/roman01la/webpack-closure-compiler)**

生产环境推荐使用devtool: 'source-map',他是独立于bundle文件的map文件,区别于开发环境的inlint-source-map

使用  new webpack.DefinePlugin({ 'process.env.NODE_ENV': JSON.stringify('production') })设置全局变量NODE_ENV,作用域bundle

> *技术上讲，*`NODE_ENV` *是一个由 Node.js 暴露给执行脚本的系统环境变量。用于决定在开发环境与生产环境(dev-vs-prod)下，服务器工具、构建脚本和客户端 library 的行为。然而，与预期不同的是，无法在构建脚本* `webpack.config.js` *中，将* `process.env.NODE_ENV` *设置为* `"production"`*，请查看* [#2537](https://github.com/webpack/webpack/issues/2537)*。因此，例如* `process.env.NODE_ENV === 'production' ? '[name].[hash].bundle.js' : '[name].bundle.js'` *这样的条件语句，在 webpack 配置文件中，无法按照预期运行。*

split css webpack 4 : mini-css-extract-plugin webpack 3 : extract-text-webpack-plugin

css压缩 :css-minimizer-webpack-plugin

## 代码分离

把代码分离到不同的 bundle 中，然后可以按需加载或并行加载这些文件。代码分离可以用于获取更小的 bundle，以及控制资源加载优先级，如果使用合理，会极大影响加载时间。

1. 入口起点：使用 [`entry`](https://www.webpackjs.com/configuration/entry-context) 配置手动地分离代码。 笨方法(重复,如果入口文件相互依赖,会被循环导入, 不够灵活)
2. 防止重复：使用 [`CommonsChunkPlugin`](https://www.webpackjs.com/plugins/commons-chunk-plugin) . 移除重复依赖的模块
3. 动态导入：通过模块的内联函数调用来分离代码。

```
ExtractTextPlugin: 用于将 CSS 从主应用程序中分离。
bundle-loader: 用于分离代码和延迟加载生成的 bundle。
promise-loader: 类似于 bundle-loader ，但是使用的是 promises。
CommonsChunkPlugin 插件还可以通过使用显式的 vendor chunks 功能，从应用程序代码中分离 vendor 模块。
```

只需配置output chunkFilename: '[name].bundle.js'即可将动态导入分离到一个单独的bundle /* webpackChunkName: "lodash" */ 命名

bundle分析

```
webpack-chart: webpack 数据交互饼图。
webpack-visualizer: 可视化并分析你的 bundle，检查哪些模块占用空间，哪些可能是重复使用的。
webpack-bundle-analyzer: 一款分析 bundle 内容的插件及 CLI 工具，以便捷的、交互式、可缩放的树状图形式展现给用户。
```

## 懒加载

懒加载或者按需加载，是一种很好的优化网页或应用的方式。这种方式实际上是先把你的代码在一些逻辑断点处分离开，然后在一些代码块中完成某些操作后，立即引用或即将引用另外一些新的代码块。这样加快了应用的初始加载速度，减轻了它的总体体积，因为某些代码块可能永远不会被加载。

只要函数是通过模块内敛分离,就会根据filename: 'bundle.[name].js',chunkFilename: '[name].bundle.js'命名格式分离chunk

## 缓存

打包生产的/dist部署到服务器上，浏览器就能够访问网站此服务器的网站及其资源。而获取资源是比较耗费时间的，所以浏览器使用一种名为 [缓存](https://searchstorage.techtarget.com/definition/cache) 的技术。可以通过命中缓存，以降低网络流量，使网站加载速度更快，然而，如果我们在部署新版本时不更改资源的文件名，浏览器可能会认为它没有被更新，就会使用它的缓存版本。由于缓存的存在，当你需要获取新的代码时，就会显得很棘手。导致代码更新了而浏览器没有去重置

设置 filename: '[name].[chunkhash].js',使打包好的文件命名不同





