# H5 & CSS3

[toc]

## H5

- 文档声明 \<!DOCTYPE html>

- \<html>元素在html5非必须,在xhtml为必须的

-  lang="en" lang="zh-CN"过时了 lang="zh-cmn-Hans">中国大陆官方用语汉语简体

- \<meta> 文档原数据 ,charset="UTF-8"字符编码

- 协议名://主机号:端口号/路径 https://localhost:80/indedx

- http默认端口80 https默认端口号为443

- 当打开的 url 协议名和原本协议名向同时,协议名可省略,//斜杠不能省略

- map和area元素

- \<figure>标记图像 \<figcaption>图像标题

- \<video>\<audio>

- 无语义化 div 语义化 header footer article section aside

- browser script可添加type=module支持esmodule

  

## CSS3

- 选择器＋声明块

- 元素select 范围太广,id范围太窄,类√

- 必须以分号结尾

- 内部,内联,外部
- user-agent 浏览器用户默认样式表,不同browser不同

- rgba() red green blue alpha hsl() 色相Hue 饱和度saturation 亮度luminance hex() 十六进制表示法 
- em ,相对父元素字体大小,递归继承,若无则使用浏览器定义的基准字号
- font-weight :normal bold  400 700 \<strong> 加粗
- font-family 可设定多个值,用户计算机必须有此字体

- font-style: italic  \<i> \<em> 倾斜
- text-decoration:line-through overline  \<a> \<del>废弃的内容 \<s>过期的内容

-  text-indent 字符 em 中文就是缩进两个字符大小

- line-height  是用纯数字,不定死,防止折叠无单位 em 百分比的区别 em 为字节的大小,当 line-height 为父值时,先继承,再计算,后面字体大小变大,line-height 也不会变大.1em=100%  在设置字体大小后再设置 em 单位是 ok 的,因为他会自动计算行高成为字体的两倍大小  纯数字就是先继承再计算
- letter-spacing 字符间距
- vertical-align 行盒居中
- background-clip:背景色覆盖区域,默认为边框盒

- visibility hidden 仍然占据空间

- background-attachment: fixed;

- \<iframe> src嵌入网页
- \<object>\<embed>嵌入flash

- MIME 多用途互联网邮邮件扩展类型
- :hover 悬停 :active 激活 :link 未访问 :visited 访问过 lvha 爱恨法则

- a:first-child 必须是 a 元素,还必须是排在 a 元素的第一个
- :first-of-type 选中 a 元素中的第一个元素
-  outline 不能设置单边,一定要设置 4 个边 outline-offset 边框偏移量
- :checked ,:diabled 被禁用时 专门用于 input:checkbox radio
- ::before ::after  ::first-letter 选中元素内容的第一个字符 ::first-line 选中元素内容的第一行 ::selection 框选的内容 ::placeholder 改变颜色
- \> 隔一代 + 下一个兄弟元素 ~ 后面所有兄弟元素
- Cascading style sheets 层叠样式 !important > 普通 > 浏览器默认

- 优先级计算 xxxx 千位内联为1 百位 id的个数 十位 类选择器,属性,伪类选择器的数量

- 盒模型 行盒,行块盒不换行,块盒独占

- margin-border-padding-content

- outline 不占据空间

- box-sizing
- overflow
- work-break:断词规则 normal(CJK文字位置截断,非CJK单词位置截断)
- white-space :nowrap 
- text-overflow:ellipsis
- 行盒 padding border margin 水平方向有效
- 空白折叠 行(块)盒之间

-  大部分非可替换元素,页面上显示的结果取决于元素内容  
- 少部分可替换元素,页面上显示的结果为元素属性
- object -fit
- 盒模型:规定单个盒子的规则   视觉格式化模型(布局规则):页面中多个盒子排列规则
- 三种排列方式  常规流,文档流,普通文档流,常规文档流 
- 块盒width会将剩余空间填满,若定宽,则margin-right:auto会将剩余空间填满

- 百分比取值 相对包含块宽度,无论是 widht,margin,padding 水平垂直都是相对于包含的宽 border 无法用百分比,包含块有高度,百分比相对于包含块,无则无效
- 常规流块盒,上下外边距相邻会合并,取max值, 左右为行快盒不会合并
- 当 border padding 为 0 时,子父元素的外边距相邻也会合并, bfc
- 浮动 常规流块盒先无视图片行块盒,接着内容的匿名行盒避开行块盒
- 匿名行盒   高度坍塌  清除浮动 clear 
- 定位 positionstatic 静态的 relative 相对定位 absolute 绝对定位 fixed 固定定位
- relative 和常规流一同排列,且移动时不影响常规流
- height:0 padding:value 背景图占据,无文字空间
- input 样式随browser变化
- textarea  resize 文本域是否能控制
- button  style: reset submit button 
- lable 显示关联分开写 id链接 隐示关联 直接卸载内部

- 表格元素:渲染速度慢,
- table caption thead tbody tfoot tr td th
- @规则  @import "path" 导入 css 文件  @charset "UTF-8"; defin浏览器该 css文件字符编码集为 必须写在 import 之前 @font-face{}指令制作一个新字体
- BFC   1.计算float高度 2.仍然无视浮动流且不会和float重叠 3. 邻边不会合并
- 等高布局

- 图片白边 1.设置父元素字体大小为 0 副作用 子元素字体消失,设置都设置不出来 2.设置图片为块盒 3.修改对齐的基线

- 参考线-深入理解字体 通常为 5 根参考线 text top/ascent 顶线  上基线 baseline 基线 sub 下基线 text bottom,descent 底线
  平时设置 font-side 字体大小是设置的文字相对大小,实际文字大小是顶线到底线的距离

- 堆叠上下文  stack context 决定了 z 轴的规定顺序

- svg  scalable vector graphics 可缩放的矢量图 1.该图片用代码书写而成的 2.缩放不会失真,类似 turtle 用代码作图 3.内容轻量
  使用方法 1.直接复制源代码  2.img backgroundimg  3.embed object iframe 

- 数据链接   优点 ,减少请求,每一次请求都是从外部获取数据
  缺点 浏览器会缓存图片  时间相应快慢说不准  用:体积较小时例如 icon  base64 将二进制转换为字符串

```
<!-- <link rel="stylesheet" href="data:text/css,h1{color:blue;}"> -->
<!-- <link rel="stylesheet" href="data:text/css;base64,aDF7Y29sb3I6Ymx1ZTt9"> -->
```

- 厂商前缀   ie 前缀 -ms-   谷歌 safari -webkit-   opera -o-   火狐 -moz-
- css hack  主要针对 ie,设置特有的样式 .特殊前缀 \*前缀,\_前缀 \9 后缀,各种兼容
- 渐进增强和优雅降级1.先写个都能运行的,再给新版本加新样式 2.先写最新的,再针对低版本处理
- 居中总结 

  - 水平方向:行盒 text-align:center 块盒 定宽 margin:atuo 

  - 垂直方向:行盒 line-height vertical align-items
  - 定位法 定大小,position,lrtb = 0,margin:auto
- 图片失效,高度坍塌,因本身是行盒,改成块盒或者行块盒即可
- border制作三角形
- box-shadow x offset yoffset blur spread color outset/inset 
- text-shadow
- background-origin 
- background-clip 
- 渐变gradient
- 径向渐变(Radial gradients)
- text-overflow  clip 裁切 ellipsis 省略号
- 2D :transform:translate(x 轴,y 轴)移动 rotate(30deg) 默认顺时针,负数逆时针  scale()比例缩放, x 轴的几倍,y 轴的几倍
- 3D: transform: rotateX(120deg); transform: rotateX(120deg); 沿着 x,y 轴翻转
- transiton 过渡
- column 创建文本排列
- 先找规律,写公共样式
- flex
- - flex container
  - - flex-direction 水平排列方向
    - flex-wrap 换行
    - flex-flow flex-direction flex-wrap
    - justify-content 主轴对齐方式
    - align-items 交叉轴对齐方式
    - align-content 多根轴线交叉轴对齐方式
  - flex-item
  - - order 排列舒徐
    - flex-grow 放大比例 默认为0 不放大
    - flex-shrink 缩小比例 默认为1缩小
    - flex-basis 占据主轴空间大小
    - flex flex-grow flex-shrink flex-basis
    - align-self 覆盖 align-items
- grid 
- text-transform: uppercase
- calc()
- position: sticky;吸顶
- over-flow auto 要想监听到滚动必须为auto

## practical skills

- BEM命名规范
- 使用css reset

- margin-left:auto 替代float right
- 无宽高, postion:absolute lrtb,拉伸铺满
- flex 多元素下水平垂直居中 flex-wrap-> align-content  or  flex-direction: column;
- line-height:n行文字  height/n
- img:max-width:100%  width:100% 兼容ie
- :not() 解决边框 问题 .div2:not(:nth-child(7n)) 

```
*{
	box-sizing:border-box;
}
:root{
	--main-color:#008c8c;
}
div{
	color:var(--main-color)
}
```

- caret-color 修改光标颜色
- -webkit-tap-highlight-color ios iphone 点击颜色
- css的锚点定位 scroll-behavior:smooth平滑滚动
- overflow-anchor 新内容载入时scroll位置
- scroll-snap 一次只滑一个元素
- touch-action:manipulation

- background-attachment: fixed; 背景图
- element 两张不同颜色堆叠
- \<picture>
