<template>
  <div id="app">
    <ele-header :seller="data.seller"></ele-header>
    <ul class="nav">
        <li><router-link to="/goods">商品</router-link></li>
        <li><router-link to="/comments">评论</router-link></li>
        <li><router-link to="/seller">商家</router-link></li>
    </ul>
    <router-view></router-view>
  </div>
</template>

<script>
import Header from './components/Header/Header'
import data from '../data.json';
export default {
  name: 'app',
  data(){
    return {
        data : {}
    }
  },
  components : {
      'ele-header': Header
  },
  /
  created(){
      this.data = data;
  }
}
</script>
<style lang="less" scoped>
    .nav {
        height: 40px;
        line-height: 40px;
        display: flex;
        justify-content: space-around;
        border-bottom: 1px solid rgba(7,17,27,.1);
        a {
            color : rgb(77,85,93);
            font-size: 14px;
            text-decoration: none;
            &.router-link-active {
                color : rgb(240,20,20);
            }
        }
    }
</style>
