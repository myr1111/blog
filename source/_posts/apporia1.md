---
title: 数据交互
date: 2019-06-05 10:36:57
tags:
- apporia
categories:
- apporia

---

# 1.***什么是跨域？跨域请求资源的方法有哪些？***
## 1、什么是跨域？
由于浏览器同源策略，凡是发送请求url的协议、域名、端口三者之间任意一与当前页面地址不同即为跨域。存在跨域的情况：
网络协议不同，如http协议访问https协议。
端口不同，如80端口访问8080端口。
域名不同，如qianduanblog.com访问baidu.com。
子域名不同，如abc.qianduanblog.com访问def.qianduanblog.com。
域名和域名对应ip,如www.a.com访问20.205.28.90.
## 2、跨域请求资源的方法：
### 1、porxy代理
定义和用法：proxy代理用于将请求发送给后台服务器，通过服务器来发送请求，然后将请求的结果传递给前端。
实现方法：通过nginx代理；
注意点：1、如果你代理的是https协议的请求，那么你的proxy首先需要信任该证书（尤其是自定义证书）或者忽略证书检查，否则你的请求无法成功。
### 2、CORS 【Cross-Origin Resource Sharing】
定义和用法：是现代浏览器支持跨域资源请求的一种最常用的方式。
使用方法：一般需要后端人员在处理请求数据的时候，添加允许跨域的相关操作。如下：
res.writeHead(200, {
"Content-Type": "text/html; charset=UTF-8",
"Access-Control-Allow-Origin":'http://localhost',
'Access-Control-Allow-Methods': 'GET, POST, OPTIONS',
'Access-Control-Allow-Headers': 'X-Requested-With, Content-Type'
});
### 3、jsonp
定义和用法：通过动态插入一个script标签。浏览器对script的资源引用没有同源限制，同时资源加载到页面后会立即执行（没有阻塞的情况下）。
特点：通过情况下，通过动态创建script来读取他域的动态资源，获取的数据一般为json格式。
实例如下：
```
<script>
function testjsonp(data) {
console.log(data.name); // 获取返回的结果
}
</script>
<script>
var _script = document.createElement('script');
_script.type = "text/javascript";
_script.src = "http://localhost:8888/jsonp?callback=testjsonp";
document.head.appendChild(_script);
</script>```
缺点：
　　1、这种方式无法发送post请求（这里）
　　2、另外要确定jsonp的请求是否失败并不容易，大多数框架的实现都是结合超时时间来判定。

---


# ***2.Axios的使用的两种方式：(详见G:/router/vue-router)***
## 1、安装：npm install axios --save
	使用：在<script>中引用：import axios from “axios”
	发送请求：
	```
	<button @click="send">发送请求</button>
	```
	```
	export default{
	methods:{
   	 send(){
      axios.get("https://api.github.com/users")
      .then(resp=>{
          console.log(resp.data);
      }).catch(error=>{
        cnsole.log(error);
      })
    }
  }
}
```

## 2、在main.js中全局引入axios并添加到vue的原型中
```
import axios from “axios”
Vue.prototype.$http=axios
<button @click="send">发送请求</button>
	export default{
	methods:{
   	 send(){
      this.$http.get("https://api.github.com/users")
      .then(resp=>{
          console.log(resp.data);
      }).catch(error=>{
        cnsole.log(error);
      })
    }
  }	
}
```
---
# ***3.ajax的使用***
## 1、Ajax的优缺点及工作原理？
### 1、定义和用法:
AJAX = Asynchronous JavaScript and XML（异步的 JavaScript 和 XML）。Ajax 是一种用于创建快速动态网页的技术。Ajax 是一种在无需重新加载整个网页的情况下，能够更新部分网页的技术。
传统的网页（不使用 Ajax）如果需要更新内容，必须重载整个网页页面。
### 2、优点：
1.减轻服务器的负担,按需取数据,最大程度的减少冗余请求
2.局部刷新页面,减少用户心理和实际的等待时间,带来更好的用户体验
3.基于xml标准化,并被广泛支持,不需安装插件等,进一步促进页面和数据的分离
### 3、缺点：
### 4、开发及性能优化
#### 1.AJAX大量的使用了javascript和ajax引擎,这些取决于浏览器的支持.在编写的时候考虑对浏览器的兼容性.
#### 2.AJAX只是局部刷新,所以页面的后退按钮是没有用的.
#### 3.对流媒体还有移动设备的支持不是太好等
### 5.AJAX的工作原理：
#### 1.创建ajax对象（XMLHttpRequest/ActiveXObject(Microsoft.XMLHttp)）
#### 2.判断数据传输方式(GET/POST)
#### 3.打开链接 open()
#### 4.发送 send()
#### 5.当ajax对象完成第四步（onreadystatechange）数据接收完成，判断http响应状态（status）200-300之间或者304（缓存）执行回调函数
### 5.ajax实例：
#### 1、引入jq:
```
<script src="http://ajax.googleapis.com/ajax/libs/jquery/1.8.0/jquery.min.js"></script>
```
#### 2、ajax:
```
$(function(){
	$.ajax({
	url:””(接口地址),
	type:”get/post”,(传值方式)
	dataType:”json/jsonp”,(跨域使用jsonp,不跨域使用json,jsonp不可用post)
	async：true/false,(是否异步)
	jsonp:”callback”（返回的函数）,
	crossDomain:true(跨域),
	timeout:(设置请求超时),
success:function(data,status)//data:数据status:状态{
	console.log(JSON.parse(data));//JSON.parse(data)//转化为js对象
}			
error:function(err,status){//err:错误
}
	console.log(err);})
})
```