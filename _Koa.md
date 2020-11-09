# Koa

基于Node.js 平台的下一代web开发框架

[toc]

## 应用

```javascript
const Koa = require('koa');
const app = new Koa();

app.listen(8080);

app.use(async ctx => {
  ctx.body = 'Hello World';
});

```

## 级联

```javascript
const Koa = require('koa');
const app = new Koa();
app.listen(8080);

app.use(async (ctx, next) => {
  const res = await next();
  res // foo
});

app.use(async (ctx, next) => {
  return 'foo'
});
```

## 设置

- `app.env` 默认是 **NODE_ENV** 或 "development"
- `app.keys` 签名的 cookie 密钥数组
- `app.proxy` 当真正的代理头字段将被信任时
- 忽略 `.subdomains` 的 `app.subdomainOffset` 偏移量，默认为 2
- `app.proxyIpHeader` 代理 ip 消息头, 默认为 `X-Forwarded-For`
- `app.maxIpsCount` 从代理 ip 消息头读取的最大 ips, 默认为 0 (代表无限)

## Listen

```javascript
const Koa = require('koa');
const app = new Koa();
app.listen(8080);
app.listen(80);

app.use(async (ctx, next) => {
    ctx.body = "hello word"
})
```

## Callback

```javascript
const http = require('http');
const https = require('https');
const Koa = require('koa');
const app = new Koa();
http.createServer(app.callback()).listen(3000);
https.createServer(app.callback()).listen(3001);
```

## Use

`app.use()` 返回 `this`, 因此可以链式表达.

```
app.use(koaBody({
    multipart: true,
  }))
  .use(cors())
  .use(router.routes())
```



## Context

可以通过编辑 `app.context` 为 `ctx` 添加其他属性。

```
app.context.foo = function(){};

app.use(async ctx => {
  console.log(ctx.foo);
});
```

## CTX

 将 node 的 `request` 和 `response` 对象封装到ctx

```
app.use(async ctx => {
  ctx; // 这是 Context
  ctx.request; // 这是 koa Request
  ctx.response; // 这是 koa Response
});
```

## API

### ctx.req

http 的 `request` 对象.

### ctx.res

http 的 `response` 对象.

绕过 Koa 的 response 处理是 **不被支持的**. 应避免使用以下 node 属性：

- res.statusCode

- res.writeHead()

- res.write()

- res.end()

### ctx.request

koa 的 `Request` 对象.

### ctx.response

koa 的 `Response` 对象

### ctx.state

推荐的命名空间，用于通过中间件传递信息和你的前端视图。

```js
ctx.state.user = await User.find(id);
```





