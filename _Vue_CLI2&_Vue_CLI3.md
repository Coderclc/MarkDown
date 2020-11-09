# Vue CLI2 & Vue CLI3

## CLI2

- --inline 默认开启,浏览器刷新应用程序启用*内联模式(inline mode)*。一段处理实时重载的脚本被插入到你的包中并且构建消息将会出现在浏览器控制台。

  ```
  log.js?4244:23 [HMR] Waiting for update signal from WDS...
  ```

  使用模块热替换的内联模式，因为它包含来自 websocket 的 HMR 触发器。轮询模式可以为替代方案但需要一个额外的入口点：'webpack/hot/poll?1000` 

- --process 将运行进度输送到控制台

- assetsSubDirectory  静态资源存放路径

- assetsPublicPath  静态资源引用路径

- proxyTable 配置代理后端规则

- "--port 8888" 修改运行端口号

- autoOpenBrowser 自启

- errorOverlay 错误覆盖全屏

- notifyOnErrors 错误通知

- poll 定制 watch 模式轮询间隔

- devtool 生成 source map

- cacheBusting  指定是否通过在文件名称后面添加一个查询字符串来创建source map的缓存 bug  vue devtools 产生bug,可将其关闭试试

- index index.html 生成路径

- productionSourceMap 生成环境的sourcemap devtool:'#source-map' 生产环境map格式

- productionGzip
  - npm install --save-dev compression-webpack-plugin 必须安装相关依赖
  - HTTP协议上的GZIP编码是一种用来改进WEB应用程序性能的技术。大流量的WEB站点常常使用GZIP压缩技术来让用户感受更快的速度。减少文件大小有两个明显的好处，一是可以减少存储空间，二是通过网络传输文件时，可以减少传输的时间。

- productionGzipExtensions 压缩那些后缀类型文件

- bundleAnalyzerReport 打包编译报告

- extract-text-webpack-plugin css分离

- path.posix.join path 模块跨平台兼容交互

- 默认不加载 postcssLoader 需配置vue-loader.conf.js loaders.usePostCSS = true

- css extraction 请只在生产环境下使用 CSS 提取，这将便于你在开发环境下进行热重载。开发环境下提取无法热重载

- ```
  ExtractTextPlugin.extract({
          use: loaders,
          fallback: 'vue-style-loader'
        })
        返回一个数组数组为拼接的所有loader
        [
    {
      loader: 'C:\\Users\\Coderclc\\Documents\\Code\\vuecli2\\node_modules\\extract-text-webpack-plugin\\dist\\loader.js',
      options: { omit: 1, remove: true }
    },
    { loader: 'vue-style-loader' },
    { loader: 'css-loader', options: { sourceMap: true } },
    { loader: 'postcss-loader', options: { sourceMap: true } }
  ]
  ```

- 