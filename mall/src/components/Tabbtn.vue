<template>
  <van-tabbar v-model="tabbarActive">
    <van-tabbar-item icon="home-o" to="/">首页</van-tabbar-item>
    <van-tabbar-item icon="shrink">专栏</van-tabbar-item>
    <van-tabbar-item icon="qr" to="/category">分类</van-tabbar-item>
    <van-tabbar-item icon="shopping-cart-o">购物车</van-tabbar-item>
    <van-tabbar-item icon="user-o">我的</van-tabbar-item>
  </van-tabbar>
</template>

<script>
export default {
  data() {
    return {
      tabbarActive: 0,
    };
  },


  mounted() {
       switch (this.$route.path) {
        case "/category":
          this.tabbarActive = 2;
          break;
        case "/":
          this.tabbarActive = 0;
          break;
          default:
              this.tabbarActive = 0;
      }
  },
};
</script>