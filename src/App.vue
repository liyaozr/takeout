<template>
  <div id="app">
    <headTop :seller='seller'></headTop>
    <div class="tab">
      <div class="tab-item"><router-link to="/goods">商品</router-link></div>
      <div class="tab-item"><router-link to="/rating">评论</router-link></div>
      <div class="tab-item"><router-link to="/seller">商家</router-link></div>
    </div>
    <router-view :seller='seller'></router-view>
  </div>
</template>

<script>
import Vue from "vue";
import axios from "axios";
import headTop from "./components/header/header";
// Vue.prototype.$ajax = axios;

export default {
  name: "app",
  data() {
    return {
      seller: {}
    };
  },
  components: {
    headTop
  },
  created() {
    axios
      .get("/apiData/seller")
      .then(response => {
        this.seller = response.data.data;
      })
      .catch(function(err) {
        console.log(err);
      });
  }
};
</script>

<style lang="stylus">
@import './common/stylus/index'
.tab
  display: flex
  width: 100%
  height: 40px
  border-1px(rgba(7, 17, 27, 0.1))
  .tab-item
    flex: 1
    text-align: center
    &>a
      display: block
      font-size: 14px
      line-height: 40px
      color: rgb(77, 85, 93)
      &.active
        color: rgb(240, 20, 20)
</style>

