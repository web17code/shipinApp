# Appdemo

> 积分银行移动端

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).

用户名正则var uPattern = /^[a-zA-Z0-9_-]{4,15}$/; 4-15位，大小写字母_-
大、小写字母、数字、特殊符号的两种及以上6-16位
密码：/^(?![A-Z]+$)(?![a-z]+$)(?!\d+$)(?![\W_]+$)\S{6,16}$/ 包含
