# Scss

## 语法格式

Sass缩进代替花括号 任何一种格式可以直接 [导入 (@import)](https://www.sass.hk/docs/#t7-1) 到另一种格式中使用，或者通过 `sass-convert` 命令行工具转换成另一种格式：

## 变量声明

变量以美元符号开头

$highlight-color: #F90;

$basic-border: 1px solid black;

## 变量引用

div{border:1px solid $highlight-color}

## 变量名用中划线还是下划线

$link-color: blue;   a {color: $link_color; } 都可以

## 嵌套

## 父选择器的标识符&

```
<div class="bullshit">
        <div class="bullshit__oops">OOPS!</div>
        <div class="bullshit--info">All rights reserved</div>
</div>
```

.bullshit{&__oops{}&--info{}}

##  群组选择器的嵌套

.container { h1, h2, h3 {margin-bottom: .8em}}

## 组合选择器：>、+和~

article {  ~ article { border-top: 1px dashed #ccc }

   \> section { background: #eee }

   nav + & { margin-top: 0 }}

## 嵌套属性

border:{style:solid;width:1px;color:#ccc;top:0;}

border:1px solid #008c8c{left: 0px};

## 导入SASS文件

对比css无需发起额外的下载请求

不需要指明被导入文件的全名

## 使用SASS部分文件

不希望sass文件单独编译成css文件

sass命名时加_ eg:themes/_night-sky.scss ,此时不会单独编译成css

@import 'themes/night-sky' 可忽略 _ ext

## 默认变量值

!default

## 嵌套导入

.blue-theme {@import "blue-theme"} 相当于将内容编译出来放到该处

##  原生的CSS导入

直接将css改成scss文件即可

## 静默注释

// /**/

body {
  color: #333; // 这种注释内容不会出现在生成的css文件中
  padding: 0; /* 这种注释内容会出现在生成的css文件中 */
}

## 混合器

@mixin name {}   @include name;

大量的重用可能会导致生成的样式表过大，避免滥用

## 混合器中的CSS规则

@mixin name {ul li {}}

##  给混合器传参

@mixin link-colors($normal, $hover, $visited) {
  color: $normal;   &:hover { color: $hover; }   &:visited { color: $visited; }  }

a {@include link-colors(blue, red, green);}  不知道对应参数顺序,含义??

$name: value 指定形参  a { @include link-colors($normal: blue,$visited: green, $hover: red  );}

## 默认参数值;

@mixin link-colors( $normal, $hover: $normal,$visited: $normal)
{color: $normal;&:hover { color: $hover; }&:visited { color: $visited; }}

@include link-colors(red)  都被赋予red

## 继承

@extend

.error { border: 1px solid red;  background-color: #fdd;}
.seriousError {@extend .error;  border-width: 3px;}

error a {...} 也会被继承到 seriouts..  a{}  

混合器把样式直接放到了`css`规则中，而继承存在样式层叠的问题

## 继承的高级用法

继承一个`html`元素的样式

.disabled { color: gray;@extend a;}

