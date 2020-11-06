# Hypertech

[toc]



##  .idea

Pycharm 生成配置文件

## Vue-i18n

http://kazupon.github.io/vue-i18n/zh/

```
// import Vue from 'vue'
// import VueI18n from 'vue-i18n'
// Vue.use(VueI18n)
const messages = {
  en: {
    message: {
      hello: 'hello world'
    }
  },
  ja: {
    message: {
      hello: 'こんにちは、世界'
    }
  }
}

const i18n = new VueI18n({
  locale: 'ja', // 设置地区
  messages, // 设置地区信息
})

new Vue({ i18n }).$mount('#app')
```

## mescroll

betterscroll?

## qs

qs.parse

qs.stringify

## vue-touch

app vue 下的this.$root.$on

axios.min.js

localStorage.getItem

## .babelrc

vue cli2 .babelrc  cli3 babel.config.js

```
presets:['stage-2']  使用 "babel-preset-stage-2": "6.22.0",babel
```

## .postcssrc.js

config autoprefixer // to edit target browsers: use "browserslist" field in package.json

Vcli2 webpack需要配置postcss-loader

## VueCookBook

## VueLoader
## d3.JS

## Echart

## hightchart

## mock

## gulp

## websocket

- [µWebSockets](https://github.com/uWebSockets/uWebSockets)
- [Socket.IO](http://socket.io/)
- [WebSocket-Node](https://github.com/theturtle32/WebSocket-Node)
- websocked
- nodejs-websocket

websocked.exe

```
./websocketd --port=8080 node ./server.js
//server.js
for(let i = 0 ;i<100;i++){
	console.log(i);
}
const ws = new WebSocket("ws:localhost:8080")

ws.onopen = function(evt) { 
    console.log("Connection open ..."); 
    ws.send("Hello WebSockets!");
  };
  // monitor i
  ws.onmessage = function(evt) {
    console.log( "Received Message: " + evt.data);
    // ws.close();
  };
  ws.onclose = function(evt) {
    console.log("Connection closed.");
  }; 

```

##  vue-lazyload 

## FastClick

```
 解决浏览器自带的wait 300ms delay to check if enlarge
  npm install fastclick import FastClick from "fastclick"  FastClick.attach(document.body)
```

