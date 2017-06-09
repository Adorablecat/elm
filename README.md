# ele

> css使用less方法需要安装 less less-loader

弹出层自改动画，不是原版

滚动效果使用scroll达不到效果，使用iscroll插件实现,但是会出现移动端默认情况下不能点击的问题，需要修改默认参数

购物车多处用到，故作为组件

对于购物车中的商品并列重复添加解决方法对商品对象添加一个属性count表示添加的数量。默认值为1，增加就count++,减少就count--

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

# run unit tests
npm run unit

# run e2e tests
npm run e2e

# run all tests
npm test
```

For detailed explanation on how things work, checkout the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
