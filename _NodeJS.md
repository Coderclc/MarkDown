# Node_JS

- 基于chorme V8 的javascript运行环境

- 中间层

-  exports 为moudle.exports的引用, 当exports = {}时,失去引用

- - ```
    var module = new Module() var exports = module.exports
    ```

- require : 先找node_modules 下的同名文件 再根据文件内的package.json的"main": "dist/jquery.js" 找到js文件,如果没有main,则找文件夹内的index.js,找不到就在node的上一级找,直到磁盘根目录.main有意外暴露内容的风险

- to.String()可将二进制转换为字符串

- Buffer 二进制形势存储,十六进制显示,内存开辟空间固定大小且连续

- 为什么不是数组,数组不能以二进制数据操作,空间不连续,存取速度慢

- Buffer.from(str) str->buffer

- ```
  const buf = Buffer.alloc(10) 开辟10个字节空间 buf[0] =255
  ```

- Buffer.allocUnsafe() 使用遗留的已存在的空间

- forEach 中的await不会等待

- cheerio 
- puppeteer
- mongoose