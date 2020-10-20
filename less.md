在浏览器环境中使用 Less ：
<link rel="stylesheet/less" type="text/css" href="styles.less" />
<script src="//cdnjs.cloudflare.com/ajax/libs/less.js/3.11.1/less.min.js" ></script>
先引入less,再引入第三方编译
node
npm install -g less
> lessc styles.less styles.css
> 将less转换成css

变量 variables
@width:100px;
@clcwidth:@width +100px;
body{
  width:@width1;
}

混合mixins
.clear-fix{
  .......
}
body{
  .clear-fix()
}
嵌套（Nesting）
.div1{
  .div2{
    & div3{
      &表示父级
    }
  }
}

CSS3 新增特性@media 查询 https://www.runoob.com/cssref/css3-pr-mediaquery.html

运算（Operations）
+ - * /
计算的结果以最左侧操作数的单位类型为准如果单位换算无效或失去意义，则忽略单位

命名空间和访问符  就是讲混入进行分组
#bundle() {
  .button {
    display: block;
    border: 1px solid black;
    background-color: grey;
    &:hover {
      background-color: white;
    }
  }
  .tab { ... }
  .citation { ... }
}

映射（Maps）
#colors() {
  primary: blue;
  secondary: green;
}
.button {
  color: #colors[primary];
  border: 1px solid #colors[secondary];
}
也和分类相同

导入（Importing）
导入”的工作方式和你预期的一样。你可以导入一个 .less 文件，此文件中的所有变量就可以全部使用了。如果导入的文件是 .less 扩展名，则可以将扩展名省略掉：
@import "library"; // library.less
@import "typo.css";