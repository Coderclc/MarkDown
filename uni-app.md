# uni-app

1. upx  375px设计稿基准宽度直接×2,将结果设为upx
2. 动态绑定中style不支持使用upx
   1. width:200upx ✔
   2. width:dynamicWidth+'upx' ✖
3. 条件编译 

- \#ifdef：if defined 仅在某平台存在
- \#ifndef：if not defined 除了某平台均存在

4.  ulist urequest   
5. uaviga 
6. 指令 @tap  綁定數據 data-  在e.currentTarget.dataset中,連接url中  採用?=形式
7. 在詳細頁面的onLoad中直接獲取
8. \<rich-text :nodes="obj.content" /> 或者 v-html 展示html格式
9. uni.showLoading({title:''}) uni.hideLoading()
10. 配置啟動項confition 