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

### 格式化

具名格式

```
const messages = {
  en: {
    message: {
      hello: '{msg} world'
    }
  }
}
<p>{{ $t('message.hello', { msg: 'hello' }) }}</p>
// 结果 <p>hello world</p>
```

列表格式

```
const messages = {
  en: {
    message: {
      hello: '{0} world'
    }
  }
}
<p>{{ $t('message.hello', ['hello']) }}</p>
<p>{{ $t('message.hello', {'0': 'hello'}) }}</p> 也能接受具名格式
```

html格式化  ! XSS攻击风险

```
    message: {
      hello: '<h1>哈哈</h1>'
    }
     <p v-html='$t("message.hello")'></p>
```

### 复数

```
const messages = {
  en: {
    car: 'car | cars',
    apple: 'no apples | one apple | {count} apples'
  }
}
$tc
<p>{{ $tc('car', 1) }}</p>
<p>{{ $tc('car', 2) }}</p>

<p>{{ $tc('apple', 0) }}</p>
<p>{{ $tc('apple', 1) }}</p>
<p>{{ $tc('apple', 10, { count: 10 }) }}</p>
```

### 日期

```
const dateTimeFormats = {
  'en-US': {
    short: {
      year: 'numeric', month: 'short', day: 'numeric'
    },
    long: {
      year: 'numeric', month: 'short', day: 'numeric',
      weekday: 'short', hour: 'numeric', minute: 'numeric'
    }
  },
  'ja-JP': {
    short: {
      year: 'numeric', month: 'short', day: 'numeric'
    },
    long: {
      year: 'numeric', month: 'short', day: 'numeric',
      weekday: 'short', hour: 'numeric', minute: 'numeric', hour12: true
    }
  }
}
const i18n = new VueI18n({
  dateTimeFormats
})

new Vue({
  i18n
}).$mount('#app')
<div id="app">
  <p>{{ $d(new Date(), 'short') }}</p>
  <p>{{ $d(new Date(), 'long', 'ja-JP') }}</p>
</div>
<div id="app">
  <p>Apr 19, 2017</p>
  <p>2017年4月19日(水) 午前2:19</p>
</div>
```

### 数字

```
const numberFormats = {
  'en-US': {
    currency: {
      style: 'currency', currency: 'USD'
    }
  },
  'ja-JP': {
    currency: {
      style: 'currency', currency: 'JPY', currencyDisplay: 'symbol'
    }
  }
}
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