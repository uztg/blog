<template>
  <div id="app">
      <!-- 返回顶部 -->
      <back-top></back-top>
      <!-- 整个视图 -->
      <router-view v-if="isRouterShow"></router-view>
  </div>
</template>
<script>
import BackTop from './components/backTop/BackTop.vue'
export default {
  components: { BackTop },
  provide () {
    return {
      reload: this.reload
    }
  },
  data () {
    return {
      isRouterShow: true
    }
  },
  methods: {
    // 定义刷新子组件的方法
    async reload () {
      this.isRouterShow = false
      await this.$nextTick()
      this.isRouterShow = true
    }
  },
  created(){
    setTimeout(() => {
      // 加载页面完后移除加载动画
      document.body.removeChild(document.getElementById('Loading'))   
    },1000)
     
  }
}
</script>
<style lang="scss">
#app {
  width: 100%;
  background-image: url(~@/assets/img/bgbg.webp);
}
</style>
