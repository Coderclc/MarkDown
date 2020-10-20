[toc]
##1.注释
<!--content-->
##2.标签/元素/标记
元素头+元素属性+元素内容+元素尾
全局属性 title  
<meta charset ="UTF-8" >
<meta charset ="UTF-8" />
文档声明<!DOCTYPE html>
html(根元素)元素在 html5 不是必须的,但是在 xhtml 是必须的,为了兼容 xhtml 还是写上吧
该元素使用的语言为 lang="en" lang="zh-CN"过时了 lang="zh-cmn-Hans">中国大陆官方用语汉语简体
meta 文档的原数据,附加信息 charset="UTF-8"网页内容编码
h1*6{} $占位符 自增
lorem 乱数假文
块级元素会独占一行  行级元素不会 老版本概念
p 段落 span 无语义  pre 预格式化文本元素  显示代码  code配合pre使用   div  模块化块级元素  span  code  div
空白折叠 超文本中的连续空白字符(空格,换行,制表),在渲染时会渲染成一个空格 
实体字符 html entity 
用于 显示特殊符号,两种方式     &单词;  &#数字;<>&lt; &gt; &nbsp;© &copy; & &amp;
记住这种格式 ((h1[id="chapter$"]>{章节\$})+p>lorem10000)*6
p.red 生成 <p class="red"></p>

a 超链接元素 3 属性
1.href="url"
2.href="#id" 有 id 回到 ID 处,无 id 到 top href="url.html # id" 3.执行 js 代码 <a href="javascript:alert('content')">a</a> 4.发邮件 <a href="mailto:804748585@qq.com"> 5.拨打电话 <a href="tel:13809233994">
target=属性
\_self 自身页面跳转
\_blank 重新开一个窗口
title 属性
对 a content 的描述

绝对路径
url:
协议名://主机号:端口号/路径
schema://host:port/path
协议名有 https http file
主机名 域名 IP 地址
端口号 http 默认为 80 https 默认为 443
当打开的 url 协议名和静态页面的 url 协议名向同时,协议名可省略,//斜杠不能省略

相对路径(./可以省略)
./当前目录
../返回上一一级 ./../

img 元素 3 属性
属性 src source 来源 alt source error 时替代
usemap="#content"
filter: grayscale(100%); 滤镜样式

map 元素
命名:驼峰或者 -
属性 name="content"

area(唯一的子元素)
target
hrmf1
coords (左上角,右下角)(所有点) (中心,半径)
shape rect(rectangle) poly(polygon) circle()
title
alt

figure 使用 <figure> 元素标记文档中的一个图像：
figcaption 有这个就不用 h 了

video 视频 MP4 webm
video <source>
controls 取值为属性名本身 布尔属性
controls / controls="controls"
autoplay / 自动播放
muted 静音播放
loop 循环

audio 音频

order list ol 有序列表
li list item 列表项
order 属性 typer=1 数字 i 罗马 a 字母 A 大写字母 reverse 颠倒
unorder list 无序列表

dl definition list 定义列表
dt definiton title  
dd definition describe

无语义化容器元素
div]

语义化容器元素
hearder<>页头 或者文章的头
footer 页脚 或者文章的脚
article 正文
section 文章的章节
aside 附加信息,侧边栏

容器元素可以包含全部
a 元素几乎可以包含全部
某些元素有固定的子元素

css 规则 = 选择器+声明块
元素选择器,选择中所有的元素名字 范围太广 h{}
id 选择器,对应 id 范围太窄 #id{}
类选择器 对应类名 .类名{}
可以对应多个类名 <p class="clas1 class2"> 重叠的时候听谁的饿呢?谁在 style 下面听谁的

声明块 ;结尾

css 书写位置 1.内部样式表 <style><style/> 2.内联样式表 <h2 style=""><> 切记分号隔开 3.外部样式表 css 文件 link

- 维护
- 响应速度
- 分离,

css 常见样式声明
为什么写的元素有样式 user-agent 有默认的自带的 元素选择器,并且在最开始
注释 /\* \*/
1.color :
:预设值 pink chocolate
/三原色 rgb 表示法(0~255)浓度越来越大  
rgb(0,255,0) a alpha 透明度 小数点 0.1 可写.1 rgba hsla
饱和度
hsl（）HSL 即色相、饱和度、亮度（英语：Hue, Saturation, Lig...
hex 表示法 #008c8c 马尔斯绿 #ff4400 淘宝红可简写 #f40 黑色#000 白色 #fff 红#f00 绿#0f0 蓝#00f 灰 ccc 青黄紫

2.background-color
3.font-size 文字大小
min-width: 最小宽度 maxheight 最大高度
max-width:最大宽度
px 像素
2em 相对值 相对于父元素的几倍 父元素字体没有大小,就找爷爷,爷爷也没有就使用基准字号(浏览器定义的大小)

4 font-weight
预设值 normal bold
数字大小 400 700
strong 元素 默认加粗

5font-family 字体  
预设值 用户计算机有这种字体才行
可设定多个值 font-family:1,2,3,4;
sans-serif 非称线字体 是一类,字体的边缘没有修饰,多种

6font-style
字体样式 倾斜
预设值 italic
i 语义化是语音阅读,实际用作图标 icon 元素 默认元素选择器 倾斜属性
em 默认倾斜

7text-decoration
加各种线
eg line-through overline
a 默认 text-decoration:underline;
del 语义 废弃的内容 默认 line-through
s 语义 过期的内容 默认 line-through

8 text-indent
预设值
像素值 px
字符 em 中文就是缩进两个字符大小

9.line-height
行间距?no 是文本的行高  
值为 px 通常都是用纯数字,不定死,防止折叠
无单位 em 百分比的区别
em 为字节的大小,当 line-height 为父值时,先继承,再计算,后面字体大小变大,line-height 也不会变大.1em=100%
在设置字体大小后再设置 em 单位是 ok 的,因为他会自动计算行高成为字体的两倍大小
纯数字就是先继承再计算

10.width
宽度
11.height
12 letter-spacing 字符间距
13 text-align
文字 的排列水平排列方式
左右 居中
对齐
vertical-align’ 特性。 ‘vertical-align’ 默认值为基线( ‘baseline ’)对齐。 改变对齐的基线 可以为 0px
baseline 该元素的与父元素的基线对齐

14 opacity(不透明度) 取值 0 到 1 整个盒子的透明度,边框内容背景
hsla rbga alpha
15.background-clip:背景色覆盖区域,默认为边框盒

16.cursor 鼠标样式 common icon image format
cursor:url("地址",auto)
cursor not-allowed 禁用

17.隐藏,隐蔽盒子
display:none
visibility 默认为 visibie hidden

18.背景图
当图片为内容时用 html 的 img 元素
当作为背景喧嚷是可用 css 的背景图样式
background-image:url("")
background-repeat no-repeat 默认 x,y 轴重复,
background-size: content cover 也可写百分比 px
background-position:center top 改变背景图在内容盒的位置
背景图背景颜色混用

精灵图 许多 icon 的合集,通过操控 background-position 还有,background-size 找到 spirit
background-attachment: fixed;相对视口固定
速写
background:url("") no-repeat center/100% color
位置在前 size 后

19.iframe 嵌入网页 src
20 object embed 在页面中嵌入 flash 可替换元素,行盒
object 两个属性 data 数据位置 type 数据类型采用 MIME 格式 多用途互联网邮邮件扩展类型 <object></object>
<embed quality="high"/> 直接在属性里传递参数,空元素 兼容性各有千秋

21<abbr title=""></abbr> 缩写词
22<time datetime="2019-5-1">2019 年五月</time> 给浏览器阅读的
23 b bold 以前是无语义元素,用于加粗字体 现用于语音阅读强调 默认为加粗
24 q (quote)引用文本,默认样式加双引号 cite
25 blockquote 大段引用文本 cite="url"
26 br 在文本中换行
27 hr 分割线
28 <meta name="keywords" content="在线商城,美容"> 给浏览器阅读的
  <meta name="author" content="chenlicheng">  name="description"  描述网站
29 link  css文件  图标   rel   relation 资源和网站的关系
<link rel="icon" href=""> 浏览器标题偷的图标  rel=" shortc icon"
放在根目录下  改名为 favicon.ico也可以

简单选择器
1.id 选择器 #id{} 2.元素选择器 元素名{} 3.类选择器 .类名{}

4.通配符选择器
_,选中所有的元素 _{}所有

5.属性选择器
选择属性
[属性名]{}选中所有属性名是这个的,[属性名="值"]{},具体化了  
class="a b c d" 空格分隔符 [class~="b"]例如包含有这种字体属性值得为什么颜色
[class^="b"]也这个值开头的属性的元素 [class\$="b"] 结尾
[class\*="b"] 包含,不用空格分隔

6.伪类选择器
:hover{}悬停时的所有  
a:hover{}悬停的的所有 a
:active{}激活状态
:link{}超链接未访问的状态
:visited{}超链接访问过后的状态
写的时候按照顺序,link->visited->hover->active 不按顺序会出错 爱恨法则 lv ha
:first-child 选择网页所有元素的第一个子元素
a:first-child 选中 a 元素中的第一个元素,错必须是 a 元素,还必须是排在 a 元素的第一个
:first-of-type 选中 a 元素中的第一个元素
对应还有 last
:nth-child :nth-of-type n 关键字 even 偶数 odd 奇数
:focus 集中 tabindex 全局属性 切换顺序  
 outline 不能设置单边,一定要设置 4 个边 outline-offset 边框偏移量
:checked 专门用于 input:checkbox radio
:diabled 被禁用时

7.伪元素选择器 在这个元素的前面,并
::before
::after
content="内容"
::first-letter 选中元素内容的第一个字符
::first-line 选中元素内容的第一行
::selection 框选的内容
::placeholder 改变颜色

选择器的组合 1.并且,直接相连 ru h2:before{} p.red 是 p 元素并且有 red 类 2.后代元素/属性/类 空格 3.子元素 > 只能隔一代 4.兄弟元素 + 这个元素的下一个兄弟元素 只会检查下一个是不是,不是就停止选择
5 兄弟元素 ~这个元素的下一个所有兄弟元素 会把后面的所有元素检查一遍

选择器的并列
多个选择器,用逗号分隔,语法糖

css 层叠样式表
声明冲突
层叠:解决声明冲突的过程 权重计算 1.比较重要性
后面 加了 !important

- !important 样式
- 普通样式
- 浏览器默认

1. 比较选择器的范围
   宽窄.选择器计算 4 位数 xxxx 越大优先级高
   千位 内联为 1,不是为 0
   百位 选择器中 id 选择器的属性 #123 #123  
   十位 类选择器, 属性,伪类选择器的数量 3.顺序
   书写代码靠后的胜利
   网上可下载的常用重置样式表
   normalize.css reset meyer

继承
子元素会继承某些父元素的 css 属性,
eg:字体相关,内容相关
inherit from body
![]()引入图片

属性值得计算
渲染每个元素的前提条件,该元素的所有 css 属性必须有值
无属性值
确定声明值 user-agent
层叠冲突
使用继承
使用默认 transparent

作者样式表
浏览器的默认样式表和默认值是不一样的
inherit 强制继承 第二部层叠就计算完毕,使用继承的值
initial 将属性设置会初始值

盒模型  
box:每个元素在页面都会生成一个矩形区域
盒子类型
行盒 css 属性 display=inline 默认为行盒
块盒 display =block
行盒页面不换行 块盒独占一行

常见行盒 span a img video audio
浏览器默认样式表快盒 容器元素 h p  
盒子由什么组成呢 从内到外 -内容 content width height -填充 内边距 padding padding-left padding-right padding-top padding-bottom  
 padding 简写属性 padding:上 右 下 左 ; 上下一样,左右一样 padding: 上 左 正方形 padding 上 -边框 border 边框样式 边框宽度 边框颜色  
 border-style 默认 none border-width 默认 0 border-color 默认字体颜色 速写属性
border:宽度 样式 颜色 -外边距 margin
margin- top margin-bottom margin-left margin-right

outline 外边框不会占据空间
内容盒 content -box 填充盒 padding-box 边框盒 border-box

盒模型应用
衡量设计稿是边框盒为整体
box-sizing : border-box content-box 选择 width,height 的对象 原先为 content-box 改为 border-box

背景覆盖范围
border-box
background-clip 改变背景覆盖范围 对象为盒模型

overflow:溢出 默认为 visible hidden 隐藏 scroll overflow-y:scroll auto 滚动条的生成与否

断词规则
word-break 绝对换行规则
normal: CJK 文字位置截断 ,非 CJK 单词位置截断
break-all 截断单词
keep-all 在空白处截断,无空白不截断溢出 overflow

空白处理
white-space :nowrap 不自动换行 pre 空白预留 <pre></pre>

text-overflow:ellipsis 省略号 不固定高度,设置不换行 css,设置 over 隐藏 设置显示 ellipsis

行盒的盒模型
跟着内容走,设置不了 width height unuseful
只能调整字体大小,类型行高 间接调整
padding 增加左右会改变结构, 上下不会改变结构 但是可以用来填充背景,填充背景都有效
border 同理  
margin 同理 左右有效
内容盒的宽高,填充盒边框盒 水平方向上的设置无效

行块盒 特殊的行盒
display:inline-block 不独占一行,但行盒无效的都有效

空白折叠发生在行盒内部 或行盒(行块盒)之间

可替换元素和非可替换元素
大部分非可替换元素,页面上显示的结果取决于元素内容  
少部分可替换元素,页面上显示的结果为元素属性
可替换元素例如 img video audio 大部分均为行盒
但是这个行盒又类似于行块盒,可以设置宽高,left right 默认 fill 时调节一个宽高会保持比例
object -fit 图片的渲染方式
contain 包含在期中 默认为 fill 直接拉伸 cover 保持比例,牺牲信息

盒模型:规定单个盒子的规则
视觉格式化模型(布局规则):页面中多个盒子排列规则
三种排列方式 1.常规流
常规流,文档流,普通文档流,常规文档流
所有元素默认为常规流
块盒独占一行,行盒依次排列

包含块(containing block)每个盒子都有包含块,决定 了盒子的排列区域
大部分盒子的包含块为父元素的内容盒 对象不同 父元素为内容盒 对对象来说即为包含块 1.块盒的总宽度为包含块宽度
width 默认为 auto,他会将剩余空间填满 auto 宽度 加 padding 加 border 加 magin=包含块
magin 为 auto 即为左右吸收,子元素居中
均为 auto 时,widht 为大

width 固定时,margin-right 吸收完剩余空间

2.块盒的高度为
内容 auto 适应内容的高度
margin 默认 auto 为 0

百分比取值 相对于包含块的宽度,无论是 widht,margin,padd 水平垂直都是相对于包含的宽 border 无法用百分比
包含块有高度,百分比相对于包含块,无则无效

两个常规流的块盒,上下外边距相邻会合并,取 max,想要隔开 100,必须都 margin100,而不是 50➕50,一定要相邻,
当 border padding 为 0 时,子父元素的外边距相邻也会合并,
重叠时 相对对象相同. 只有上下会 ,左右不会

2.浮动
文字环绕
是因为常规流块盒先无视图片行块盒,接着内容的匿名行盒避开行块盒
横向排列
float 属性
left 靠上靠左 right 靠上靠右靠默认 none
设置 float display 强制转为 block
这个 block 不独占一行
宽度为 auto,适应内容的宽度
margin auto 为 o
对比行块盒,块盒的浮动没有空白折叠间隙
排列时回避开常规流的块盒
常规刘块盒排列时,无视浮动流块盒,书写顺序决定
行盒排列时会避开浮动盒
匿名行盒.所有的文字都会被浏览器放在一个行盒中
高度坍塌,常规流的适应内容高度 auto 不会计算浮动流盒子的高度
清除浮动 clear 默认为 none left:清除左浮动,right 清除右浮动 both 清除左右浮动,
该元素会出现在所有 left right both 盒子的下方
写一个空元素 div clear
通常用.clearfix::after{content=" clear" display=block clear=both 默认为行盒想想书名号}
over-flow=hidden 浮动元素又回到了容器层，把容器高度撑起 BFC

考虑整体样式,放大思维
左浮动向上向左排列 右浮动向上向右排列
空间不够向下移动知道空间够了再水平移动,浮动盒子的顶边不能高于上一个盒子的顶边

3.定位
手动控制元素精准定位
position  
static 静态的 relative 相对定位 absolute 绝对定位 fixed 固定定位
定位元素会脱离常规流
relative 除外 relative 排列还是会和常规流一起排列,但是移动时不会影响常规流元素
常规流排列会忽略那些脱离了常规流的元素
relative
不会导致元素脱离文档流,只会让元素在原来的位置偏移
left right top bottom
盒子的偏移不会影响其他常规流元素
absolute 他的包含块不是他父元素的内容盒了,祖先元素第一个定位元素的填充盒,否则为整个网页的,初始化包含块
他的活动范围包含块,leftright 为距离左边的距离
fixed 固定定远的包含块为 视口,浏览器的可视窗口
绝对定位,和固定定位居中,定宽定高,
leftrighttopbottom 为 0 全部初始化,margin auto
定位元素重叠时,堆叠上下文,
设置 z-index value 越大,越靠近 user,只有定位元素才有效,可以设置为负数,-1 被常规流和浮动覆盖
绝对,固定定位的元素一定是块盒,relative 不会改变
排列方式,不可能是多种,即浮动又定位
固定定位宽度要设置成 100%定宽

1.给 nav 定型,让 nav 在 div 中 marginauto 居中 2.直接让整个 nav 里的内容 textaligncenter 居中,可继承. line-height 水平
样式切换,可以切换类 active 的位置 javascript 中
因为随着浏览器缩小,宽度没变,证明不是百分比,所以定宽
插入一个列表 ulli 只不过表示这里有一个列表,只是为了解读,不影响结果
老师采用的是都浮动,定宽,防止串行
我采用的是常规流无视浮动流,内容避开浮动流
当浮动和行盒在同一行时,浮动在后也会跑到最前方,然后行盒避开
行块盒是特殊的行盒,只有一行
border-radius: 15px;
:nth-child()伪类选择器 n 为自然数 p::nth-child()是 p 且第几个 p p :nth-child() p 的第几个后代
white-space: nowrap;
overflow: hidden;
text-overflow: ellipsis;
text-align: center;
一套组合拳
切记有浮动之后都要 clear 以防万一
display=none 让这个块不显示
一种逻辑思维,在一个小的框里放多的东西,让他溢出
在表示图标的图片中隐藏一个一级标题 h1 让他溢出

表单元素
一系列元素,用于收集用户数据

input 元素 输入框
type: 输入的类型 text 普通文本 password 密码用\*代替 date 日期建荣文 search 搜索兼容 image 图片
range 滑块 color 色彩框 number 只能输入数字框 checkbox 多选框 radio 单选框 checked 初始选择 file 文件
value:初始显示值 placeholder="请输入密码"占位符
input::-webkit-input-placeholder 修改颜色
max-length

input make button
type:submit button reset

select 元素 子元素 option 选择 选项 可加布尔属性 selected 初始选择 布尔属性 multiple

<optgroup label></optgroup> 给选项分组

textarea 文本域 row 行 col 列 css 属性 resize 控制文本域是否能被控制大小
text ,textarea 首行缩进 padding 还有 text-indent 首行缩进

button
style: reset submit button 默认为 submit 文本直接写在 button 内容 不用写在属性所以可以加图片等

配合表单使用的元素
label 通常配合单,多选框使用
显示关联 label inputradio 分开写 隐示关联 直接把 inputradio 写在 label 中
作用是点文字也能切换,点标签也能切换

datalist 数据列表
通常用与和普通列表一起使用 <datalist id="user"> list id data 下写 option value 值对应

form 通常将整个表单元素放到 form 中,当提交表当时,会将表单以合适的方式提交到服务器 fo

fieldset 表单分组 字段集
子元素 legend 元素 表单分组标题

表单状态
布尔属性 readonly 只能读 disabled 是否禁用
溢出的加滚动条,设置类属性以后可以用 js 切换

表格元素
杂碎太多渲染速度太慢,全部读取完毕才渲染
表格 table  
caption 表格标题 thead 表头 tbody 表格主体 tfoot 表尾
thead tbody tfoot 都有的子元素 tr trow 表格行
普通单元格 td thead 的单元格 th table width:100%可继承 border-collapse 默认 separate
td colspan=""跨越多少列 rowspan="跨多少行"

@规则
at-rule @规则 @语句 css 语句 css 指令 书写与 css 中
import
@import "path" 导入另外一个 css 文件 @import "reset.css"; 分号结束 先导入这个
@charset "UTF-8"; 告诉浏览器该 css 文件的字符编码集为 必须写在第一行,在 import 之前
@font-face{}指令制作一个新字体

web 字体和图标
web 字体 用户电脑没有这个字体,强行让用户下载
iconfont.cn link 外部 CSS 文件
font-class 方式
类名创建 link href 在线使用 类名 after 使用
离线使用 下载文件
unicode 方式
复制字体创建,修改字体 使用实体字符 html entity &#16 进制数字
icon 两种方式,精灵图 css 指令

block fotmatting context BFC
它是一块独立渲染的区域,规定了常规流块盒的布局

- ,水平方向上,总宽度=包含块的宽度
- 垂直方向依次排放
- 外边距无缝相邻,外边距合并
- 排列时无视浮动元素
  根元素,hmtl 创建的 bfc 覆盖了网页中的所有元素
  浮动和绝对定位,固定定远 元素
  overflow!=visible 的块盒
  主要是利用它的特性,他的规则 ,
  会创建 bfc 创建这个渲染区域的元素,auto 高度会计算 float 块盒的高度,但还是不会计算定位流的高度
  创建 bfc 区域的元素,还是会无视浮动流,它是区域会避开浮动流,不会重叠
  bfc 区域内不会发生邻边合并

  布局 1.主区域定宽,浮动, 2. 利用常规流块盒 bfc 区域会避开浮动
  两栏三栏一样

  等高布局
  1.CSS 的弹性盒
  2.js 控制 3.伪等高 由主内容来决定外边框的高度,所以 afterclear 产生的必须在主内容下,
  侧边栏设置夸张的高度,height10000;再设置 margin--bottom 为负数 原理
  产生的效果为,侧边栏的背景填充高度由主栏决定
  为什么呢 因为外框的自动适应高度为适应这个盒子 内边框的 width+padding+margin+border margin 为负数,外框也变小

  元素书写顺序,
  float 先 float 再主题
  定位 先主题 在绝对定位 祖先元素&定位元素的填充盒

  后台页面的布局 为了改变视口大小的时候不产生滚动条,里面产生滚动条
  整个页面不会发生滚动,那么整个页面的大小百分比要随着视口的大小发生变化
  整个页面放进一个容器 fixed 视口
  内容也要为 100% 100%,的话,把标题绝对定位,给内容设置 padding

body 的拓展
backgroud-color 填充的是边框盒
画布 canvas

设置 html 或者没设置 html 设置 body background color 时设置是画布,画布取决于 html,有最小值最小值为视口的宽高

background-image
body 设置背景图
设置 html 或者没设置 html 设置 body background-image 宽高百分比相对于 html 没有最小值
恢复正常给 html 加点颜色就好了

行盒的垂直对齐
多个行盒垂直方向上的对齐
图片的底部白边

当图片的父元素块盒的高度是自动时,图片盒父元素底部有白边 图片的基线在最图片 1.设置父元素字体大小为 0 副作用 子元素字体消失,设置都设置不出来 2.设置图片为块盒 3.修改对齐的基线

参考线-深入理解字体
font-size line-height vertical-align font-family
文字的制作时有参考线的 不同文字参考线不同
通常为 5 根参考线 text top/ascent 顶线 super 上基线 baseline 基线 sub 下基线 text bottom,descent 底线
平时设置 font-side 字体大小是设置的文字相对大小,实际文字大小是顶线到底线的距离

堆叠上下文
堆叠上下文 stack context 绝对了 z 轴的规定顺序

- html 会创建堆叠上下文
- 设置了 z-index 的定位元素 except z-index auto

svg
svg scalable vector graphics 可缩放的矢量图 1.该图片用代码书写而成的 2.缩放不会失真,类似 turtle 用代码作图 3.内容轻量
使用方法 1.直接复制源代码
2.img backgroundimg
3.embed object iframe

书写 svg 默认 300×150
矩形 rectangle rec
width height x y 距离 xy 的距离 fill 颜色 stroke 边 stroke-width 边
圆形 circle cx="中心店的坐标" cy
transparent 透明
椭圆 ellipse rx"长半轴" ry 短半轴 cxc cy
线条 line
x1 x2 y1 y2
polyline 多线<polylne points=""> 设置点 会自动把第一个点和最后一个点相连填充
polygon points=""
<path d="<path>"> 路径

数据链接
data url data:MIME, 加数据
意义??
优点 ,减少请求,每一次请求都是从外部获取数据
有利于数据动态变化
缺点 浏览器会缓存图片
时间相应快慢说不准
应用:体积较小时例如 icon

base64 将二进制转换为字符串

<!-- <link rel="stylesheet" href="data:text/css,h1{color:blue;}"> -->
<!-- <link rel="stylesheet" href="data:text/css;base64,aDF7Y29sb3I6Ymx1ZTt9"> -->

浏览器的兼容性
市场竞争,版本变化,厂商前缀
eg box-sizing -webkit-box-sizing 自己弄的属性
ie 前缀 -ms-
谷歌 safari -webkit-
opera -o-
火狐 -moz-

-webkit-特有滚动条
背景图多选一
background-image:-webkit-image-set(url()1x,url()2x)浏览器会自行选择 1x 一个像素点有一个显象单元

css hack
根据不同的浏览器,主要针对 ie,设置不同的样式和元素 1.样式
ie,中 css 特殊前缀 \*前缀,\_前缀 \9 后缀,各种兼容

渐进增强和优雅降级 1.先写个都能运行的,再给新版本加新样式 2.先写最新的,再针对低版本处理

居中总结
行盒行块盒居中
水平居中 text-align-center
块盒 定宽 margin auto
定位块 lrtb=0,margin=auto

垂直
行块盒或块盒里面的单行盒,line-height vertical
行块盒或块盒里面的多行盒 没完美方案,给盒子设置相同的 padding

样式补充
display :list-item
本质是一个块盒,该盒子会附带一个盒子
盒子本身是 主盒,生成的为次盒 先排列次盒
ulli 即如此
设置 css list-style-type 这个属性可继承
list-style-position 次盒相对主盒位置
list-style:速写 circle inside;

图片失效时的宽高问题,坍塌,img 本身是行盒,改成块盒或者行块盒即可

行盒中包含行块盒和可替换元素 行盒高度只跟字符有关,行块盒,img,等撑不起行盒,把这些元素换成块盒

text-align:justify
justify 除了最后一行外,分散对齐,把空白撑开 最后一行也实现::after

制作一个三角形
利用边框,width,height=0,其他颜色为透明

direction 方向 writing-mode
direction 设置开始和结束的方向 ltr left to right
writing-mode vertical-rl

utf-8 直接书写
&#x0000;&#x0000; 写在 content 里面 content:"\0000"

项目开发注意事项 1.重视项目

CSS3
盒阴影 box-shadow
5 个值 +-x 沿着 x 轴的矢量 +-y 轴 +模糊度 扩大的像素 颜色 默认 outset
x offset yoffset blur spread color outset/inset 建议大小为 20px

text-shadow
x offset yoffset blur colora

border-images
border:15px solid transparent;

background-images
background-Origin 背景图像的区域, border-box contentbox
background-clip 裁剪后显示的区域 显示 border-box

渐变 gradient
background-image: linear-gradient(to top ,#fff,#000); 起点,终点颜色,角度 deg
to left right ,bottom right deg
多个颜色节点 依次写 background-image: linear-gradient(to right, red,orange,yellow,green,blue,indigo,violet);  
颜色可设置 hsla rgba 带透明度的调色
转换节点
linear-gradient(red 0%, orange 25%, yellow 50%, green 75%, blue 100%);
红完全转换为橙是在 25,转换中点是 12.5
linear-gradient(red 10%, 30%, blue 90%);
0~10 为纯红,从 10 开始到 90 为 gradient 90~100 为纯蓝,默认转换节点是中点那就是 90-10/2,中点为 50,中间的 30 为设置了转换节点
重复线性渐变, background-image: repeating-linear-gradient(red, yellow 10%, green 20%);

径向渐变(Radial gradients)
closest-side closest-corner farthest-side farthest-corner
与最近的边

text-overflow
clip 裁切 ellipsis 省略号

word-break: keep-all; break-all 强制截断 控制单词的截断
word-wrap 控制 换行 break-word

css3
2d 转换
transform:translate(x 轴,ya 轴)移动
rotate(30deg) 默认顺时针,负数逆时针
scale()比例缩放, x 轴的几倍,y 轴的几倍

      2、skew(xdeg,ydeg)
         ydeg : 纵向倾斜度数
         y取值为正，y轴不动,x轴顺时针倾斜一定角度
         y取值为负，y轴不动,x轴逆时针倾斜一定角度

         matrix矩阵
          a,b,c,d,e,f
          结论 e对应x轴位移,f对应y轴位移
          a对应x轴缩放，d对应y轴缩放

3d 转换
transform: rotateX(120deg); transform: rotateX(120deg); 沿着 x,y 轴翻转

transiton
transition: width 2s;过渡

css 动画
@keyframes myfirst
{
0% {background: red; left:0px; top:0px;}
25% {background: yellow; left:200px; top:0px;}
50% {background: blue; left:200px; top:200px;}
75% {background: green; left:0px; top:200px;}
100% {background: red; left:0px; top:0px;}
}
或者用 from to
animation myfirst 2s

css3 创建多列排列
column-count: 3; 创建 3 列
column-gap: 40px; 间隙 40px
column-rule-style: solid;
column-rule-width: 1px;宽度
column-rule-color: lightblue;颜色
column-rule: 1px solid lightblue;
column-span:all 跨越多少行
column-width: 100px; 定宽

外形修饰
outline:2px solid red;
outline-offset:15px; 偏移 正负外内

按钮动画添加箭头标记:,把图标 o'pcity 从 0 到 1
按钮动画点击时添加 "压下" 效果: 影子
按钮动画波纹效果 从 1 到 0,从无到有

选择器前加 not 排除 not(.active)
分页
做到无缝 a 为行盒,且无空白折叠, 浮动
ul>li 行块盒>a 行盒设置 padding 行块盒都能设置

CSS3 弹性盒（ Flexible Box 或 flexbox），是一种当页面需要适应不同的屏幕大小以及设备类型时确保元素拥有恰当的行为的布局方式
行块盒
同一行设置,设置 margintop,bottom 整行都会动
行盒里面放行盒因为宽度不够会换行 white-space :nowrap
设置 lineheight 要注意,继承属性,vertical 要当心
常用方法,全部框起来,设置整体 margin-top
h1 标题,设置 apadding,仍然有背景图,height 为 0 内容隐藏, 第二种,a 为块盒,内容在第二行,隐藏

用 form 框起来,buttonsubmit,回车提交
text-indent

使用公共样式,整体统一,
多使用伪元素选择器
伪类选择器,找规律
利用 text-align= justifyl
在最下方生成宽度拉满,高度为 0 的块
命名,最外边命名,多用外名,里面用通用的,生成的都用伪类来写
处理空白折叠,利用浏览器自动在最后出生成</>取消空白折叠
用浮动会出现高度不统一时的问题,定高可以解决
每一次设置并排电影图片浮动 margin 时,记得设置转行的为 0  
设置最大的宽度为 max-,让他自适应
行块盒也自带 bfc
判断切换的位置,
一些简单的可以直接 hover 后写,生成  
多写注释

兼容 ie8 的透明度
filter:alpha(opacity=50)

nth-给第 5n 个设置 margin-left 为 0 或者给父元素设置一个负的 marginright

flex container flex item 弹性盒 弹性盒的项目  
display: flex inline-flex 决定了弹性盒为块级还是行级
container dispaly=flex flex item 水平布局
flex 布局模型 main axis 主轴 cross size 交叉轴  
 main start 主轴开始 main end 主轴结束 cross start cross end  
 main size 即水平方向的宽 cross size

## flex-container

flex-flow
缩写属性
flex-direction||flex-wrap
flex-direction
flex-item 强制转换为 block 默认为 row 排列 main start->main end
value:row-reverse column, column-reverse column 不是 across 排列方向,而是将主轴变为 column

flex-wrap
默认情况 flex-items 为单行,即使大于 flex-container,执行 compress
nowrap 默认为单行 wrap 多行 wrap-reverse 对比 wrap cross start 和 end 方向相反

justify-content
调整 flex-item 在 main axis 的对齐方式
flex-start flex-end center space-between 两边贴边 space-evenly 均分 space-around 左右的距离是中间的一半

align-items
调整 flex-item 在 cross axis 的对齐方式 justify 单行对齐方式
items 在 cross axis 是拉伸满的
normal == stretch

align-content
justify 调整多行 items 对齐方式
flex-start flex-end

## flex-items

flex
flex-grow |flex-shrink|flex-basis
缩写属性

order
设置为 value,justify 排布顺序
defalut 默认值是 0 可以为负数

flex-basis
设置 main-axis 方向上的 items 的大小 ,即 width column 即 height

flex-grow
自动拉伸,value 为 number 可以为小数,即不全部分完

flex-shrink
默认值为 1,默认就会收缩

align-self
会覆盖 align-items 的 effort 设置单独的 align-items


Grid 布局
display:grid display:inline-grid

grid-template-columns: 40px 50px auto 50px 40px;
grid-template-rows: 25% 100px auto;
inline-grid rows columns auto 无效 columns auto 无效
可以指定名字
grid-template-columns: [cross1]80px [cross2]40px [cross2]10px [cross4]40px;
grid-template-rows: [main1]30px [main2]60px [main3]90px;
划线分布
grid-column-start: cross1;    grid-column-end: cross4;

grid-template-columns:repeat(2,100px 20px)  2个100px+20px 
repeat(auto-fill 100px) 在一行内放满100p'x
1fr 1fr 2fr;  按比例划分 ,三行或者三列 ,后面的为前面的两倍  fragment


布局下的div默认按照格子的顺序从做左到右分布,大小就是格子大小
grid-template-areas: "header header header header"
                            "main main empty sidebar"
                            "footer footer footer footer";
给每个格子都命名, 
grid-area: header; 占据格子
grid-area: <row-start> / <column-start> / <row-end> / <column-end>;
grid-area: 1 / 1 / 3 / 3;  也可划线

grid-line grid-column-start: 2;grid-column-end: 4;
grid-row-start: 2;grid-row-end: 4;  
划线,根据线来起止
grid-column:  2/4 ;=grid-column-start: 2;grid-column-end: 4;
  grid-row:  / 


内对齐
justify-items:start | end | center | stretch;  水平方向
网格内的div默认会撑满,当设置了大小小于网格大小,justify-items就是div在网格内的对齐方式
align-items start | end | center | stretch;   垂直方向
justify-self start | end | center | stretch; 操控单个单元格
align-self  :
place-items = <align-items> <justify-items>; centent;center
place-self  <align-self> <justify-self>;  设置单个]

外对齐 容器相对于浏览器对齐
place-content :<align-content> <justify-content>
start | end | center | stretch | space-around | space-between | space-evenly;
space  格子拆分对齐

间隙
column-gap:10px
row-gap:10px
grid-gap:  <grid-row-gap> <grid-column-gap>; 20px 20px; 速写attr

默认填充是先行后列   可以改为先填充列  grid-auto-flow: column;

 <video
      data-dps-name="default_"
      name="media"
      muted
      autoplay
      loop
      class="dps video-bg dps"
      poster="./about01.jpg"
    >
      <source
        type="video/mp4; codecs=&quot;avc1.4D401E, mp4a.40.2&quot;"
        src="./test2.mp4"
        group="banner"
      />
    </video>
放动图

想要重复的触发动画必须先显示5s,再隐藏0s,不可以直接频繁显示,只写显示不写隐藏不能重复
text-transform: uppercase; 全部大写
letter-spacing: 2px;
div1{div2} div1,div2设置4条边,设置width 100%
