# Webpack

[toc]

```
4.0 以下              webpack   ./src/index.js     ./dist/bundle.js    ->bundle.js
4.0 以上还需要webcli    webpack   ./src/index.js -o  ./dist              ->main.js
```

## 安装

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

### 管理资源

在 webpack 出现之前，前端开发人员会使用 grunt 和 gulp 等工具来处理资源

use: [ 'style-loader', 'css-loader' ]顺序很重要,加载顺序为从右到做

1.  加载Css  [style-loader](https://www.webpackjs.com/loaders/style-loader) (将css-loader内部样式注入到我们的HTML页面)和 [css-loader](https://www.webpackjs.com/loaders/css-loader)(加载.css文件)：
2. file-loader,加载图片,字体并转存到dist文件夹下
3. 当文件较小时可使用`url-loader` 功能类似于 [`file-loader`](https://github.com/webpack-contrib/file-loader)，但是在文件大小（单位 byte）低于指定的限制时，可以返回一个 DataURL。

4. 加载数据如JSON 文件，CSV、TSV 和 XML使用[csv-loader](https://github.com/theplatapi/csv-loader) 和 [xml-loader](https://github.com/gisikw/xml-loader)。让我们处理这三类文件：

## 管理输出

使用HtmlWebpackPlugin html可自动关联打包好的js文件

使用[`clean-webpack-plugin`](https://www.npmjs.com/package/clean-webpack-plugin)清理文件夹

webpack及其插件似乎“知道”应该哪些文件生成。答案是，通过 manifest

## 开发

