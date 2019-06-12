---
title: 个人扩展
date: 2019-06-05 08:05:18
categories:
- personal
tags:
- personal
notshow: true


---

# 1.***移动端自适应flexible的使用***
## (1).引入cdn:
```
<script src="http://g.tbcdn.cn/mtb/lib-flexible/0.3.4/??flexible_css.js,flexible.js"></script>
```
## (2).引入js\css
(详见G:/习题资料/flexible)
## (3).1rem=75px



---



# ***2.vue-cli整理：(详见G：vuecliTest)***
## 1、vue init webpack-simple  文件夹名
## 2、找到所在的G:cd 文件夹名称(vuecliTest)
## 3、npm install
## 4、npm run dev
## 5、http://localhost:8080



---



# ***3.vue 路由：(详见G：/router/user)***
## 1、http://localhost:2333/xxx?a=1&b=2#app
http: protocal 协议头（伪协议）
Localhost:hostname(主机名)
2333:port(端口)
Xxx:pathname(路径）
a=1&b=2:search(查询参数)
app:hash(定位锚点)
## 2、改变url不向服务器发送请求
监听url变化
解析url信息并执行相应操作
## 3、hash与history:
hash:(window.location.)
assign:生成一条历史记录，改变浏览器的地址
replace：不能生成新的历史记录，改变浏览器的地址
onhashchange:监听hash值的改变
history:(window.history)
pushState:生成一条历史记录，改变浏览器的地址
ReplaceState:替换当前历史记录，改变浏览器的地址
注：两者改变的是真实路由，不会向服务器发送请求
Onpopstate:监听history值的改变
## 4、安装：
cnpm install vue-router -S
## 5、基本用法：使用router-link组件来定义链接，to属性指定链接url
router-view用来显示路由内容
```
<div>
<router-link to=”/home”></home>
</div>
<div>
<router-view></router-view>
</div>
```
## 6、定义组件：
Var home={
Template:”<><>”
}	
## 7、配置路由：
```
Const routes=[
{
Path:”/home”,
Component:home
}
{
	Path:”/user”,redirect:”/home”//重定向
注：(path:”/a”,redirect:”/b”)//从a页面重定向到b页面
}
]
```
## 8、创建路由实例：
```
Const router=new VueRouter({
	Routes，
	Mode:”history”//更改路由模式
	linkactiveClass:”active”//更改活动链接class类名
})
```
## 9、创建根实例并将路由挂载到vue实例上
```
New Vue（{
El:
Router:router//注入路由
}）
```
## 10、路由嵌套与参数传递：
传参的两种形式：
查询字符串：login？Name=tom&pwd=123
rest风格url:regist/alice/123
路由实例的方法：
Router.push()添加路由与router-link相同、切换路由
Router.replace()替换路由，没有历史记录



---



# ***3.element-ui:(pc端)***
## 1、安装：npm install element-ui --save
## 2、在main.js中引入并使用组件
```
import ElementUI from "element-ui"
import 'element-ui/lib/theme-chalk/index.css'（单独引入css样式）
```
注：此方法引入了所有组件
## 3、使用：Vue.use(ElementUI)
## 4、在webpack.confing.js 中添加loader：
css样式和字体需要由相应的loader来加载
		cnpm install style-loader --save-dev
	    cnpm install css-loader --save-dev
	    cnpm install file-loader --save-dev
		修改webpack.config.js文件


---



# ***4..mint-ui使用（移动端ui）***
npm install mintui -save
在main.js中按需引入：
注：要引入css:import 'mint-ui/lib/style.css'
详见：http://mint-ui.github.io/#!/zh-cn



---


# ***5.animate.css的使用***
## 1、引入文件：animate.min.css
## 2、使用：
```
<div class=”animated 样式名称” id=”ys”></div>
```
## 3、通过jQ应用：
```
$(function(){
$(“#ys”).mouseover(function(){
$(this).addClass(“animated 样式名称”);
})
注：如果需要延迟执行，可使用setTimeout()
Eg:setTimeout(function(){
$(“#ys”).addClass(“animated 样式名称”)
},3000)
})
```


