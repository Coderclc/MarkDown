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

