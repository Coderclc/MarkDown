# jQuery 
## write less do More!  同一$()可进行多线程操作
<script>
jQuery
1. 1.x兼容老版本IE 文件过大 2.x部分ie8以下不支持,文件小,执行效率高  3.x完全不支持ie8,提供了api
jQuery核心函数  $/jQuery  核心对象 $()/jQuery()   jQuery的对象命名前常➕$
2.$(param)  
params 为函数 (当dom 加载渲染完,执行此回调匿名函数)
params 为选择器字符串  查找所有的标签,将对应的dom对象其封装为jQuery对象并返回
params 为dom对象 将dom对象封装为jQuery对象并返回
params 为html标签字符串,创建标签对象并封装为jQuery对象
$.property
$.each() 隐式遍历数组     $.each(arr,function(index,value){})    
$.trim()去除两端空格      $.trim(str)
3.$("#app").click(function(){$(this).html()})中this指向的是dom对象 所以事件的函数不建议使用箭头函数,找不到this
4.html()	读或写被选元素的内容
5.$().appendTo("#div")
6$()是一个伪数组,伪数组中的元素是dom对象,可用$.each(arr,fn),jqarr.each(fn),原生for()遍历
7 $().length ,.size() 已失效 ,获取伪数组长度
8 获取伪数组的元素,$("div")[index]   $("div").get(index)
9 $().index()  具体的某一个jquery对象在其他兄弟对象的index
10 伪数组,为obj,即key为number,添加了一个属性为obj.length
11原生js操作的是dom对象,$()操作的是$()对象中的所有DOM对象
12 Selector  
$("div") all tag name div
$("#div") id = div
$(".div") class = "div"
$("div,span") all tag name = div and span
$("div:not(.box)") in div class not box  无class也为没boxclass
$("li:gt(0):lt(2)")  大于index0,小于index3,从0开始 按顺序执行
$("li:eq(3)")列表中的第4个元素
$("li:contains('BBBB')")内容包含
${":input,:checkbox"} 一些特殊的表单选择器  :text  :password
$()事件中this指的为触发事件的dom,把this 传入$()得到dom对象的$()对象
$().attr("property","value")  读写属性值 移除  $().removeAttr("name")remove attr
$().prop("property","value") 同attr ,opera boolean type  
$().addClass("")不会覆盖   $().removeClass()  移除   toggleClass() 
$().html()  ==innerHtml   ().html("<h1>h1</h1>") 读写内容
$().val()  获取value值   $().val("chenlciheng")   set
$().css("color","value") 读,写, 填对象即为写
$().offset().left .top  相对于视口左上角的位置  多元素时为第一个 可设置传{top:number,left:number}
$().position() .left .top 相对于定位元素的填充盒左上角的坐标
$().scrollTop(value) 获取滚动条距离顶部的距离,传值set  获取ie/chrome对象不同 ,body|html
$().height() $().width()  内容盒   可读可写
$().innerHeight() $().innerWidth() 填充盒  可读可写
$().outerHeight(false/true) $().outerWidth(false/true)   边框盒/边框盒加margin  可读可写
$().first() 筛选过滤 $()对象  $().last()    第n(index+1)个  $().eq(index)
$().filter("[class=app]") $().not("[class=app]")$().has("span")  有span tag 都是同等的选择器方法
$().children(":fitst") gather   可传进一步过滤set  子元素  $().find(":fitst")  后代元素
$().parent() $().parents()所有的祖先集  $("span").parentsUntil("div");共同的祖先
$().siblings(), 所有同胞,不需要相同元素  $().next() 下一个同胞  $().nextAll() 后面所有的同胞  
$("h2").nextUntil("h6");   之间的同胞   prev(), prevAll() & prevUntil()  相同
$().append("<h1>123</h1>") add in last  $("<h1>123</h1>").appendTo($())生成标签,插入到 
$().prepend("<h1>123</h1>") add in first  $("<h1>123</h1>").prepend($())生成标签,插入到 
$().before()  $().after()   之前之后插入 $().replaceWith("new tag")替换 replaceAll("selector")old
$().empty() ul>li 杀li   $().remove("filter") ul>li ul也杀 
$().click()  $().on("click",fn)   $().mouseleave()  $().mouseenter() $().on("mouseenter",fn)
$().hover(fn(enter),fn(leave))  $().off() 解绑所有监听 $().off("click")  on对应的字符串
事件都可传event   clientX,clientY 相对于视口  pageX,pageY,相对于页面,offsetX,offsetY相对于事件el
停止事件冒泡 event.stopPropagation()  prevent 事件默认行为 event.preventDefault()
mouseover,mouseout  会事件向下绑定,  对比 mouseenter mouseleave  不会发生绑定 
 $("#div").delegate("li","click",fn(){})事件的委派,对应event.target$("#div").undelegate("click")
$().fadeOut("slow","normal","fast",) 3params speed effort(easing),default(swing,/linear),callback
$().fadeIn() $().fadeToggle()   $().slideUp() $().slideDown() $().slideToggle() 
no animation  $().show() $().hide() $().toggle()
custom animate  $().animate({attr:number/"numberpx"/"number"},ms)  top:"+=300" 当前位置increment
$().stop()
release $ jQuery.noConflict()
window.onload(fn) 文档,图片全部加载完执行 只能有一个监听
 $(document).ready(fn) 文档加载完就执行 可以有多个监听
 Plugin:拓展$的方法 (function(){$.extend({})})()
        拓展$()的方法 (function(){$.fn.extend({})})()