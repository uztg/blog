<template>
  <div>
     <div id="top" class="backTop" @click="BackTop()" v-show="flag" style="background-position-x: -898px;"></div>
  </div>
</template>
<script>
export default {
      data() {
      return {
        flag:false
      }
    },
  methods:{
    BackTop(){
     // 页面pc端滚动
      window.scrollTo({ 
        top: 0, 
        behavior: "smooth" 
      });
      // 移动端滚动
       let timer = setInterval(() => {
        document.body.scrollTop-=50;
        if(document.body.scrollTop <= 0) {
          clearInterval(timer)
        }
      },10)
    },
  },
  mounted () {
      window.addEventListener('scroll', (() => {
        if(document.body.scrollTop >= 100 || window.pageYOffset >= 100 || document.documentElement.scrollTop >= 100){
          this.flag = true;
        }else {
          this.flag = false
        }
      }),true)
    }
}
</script>
<style lang="scss" scoped>
 .backTop {
   position: fixed;
   right: 50px;
   bottom: 100px;
   cursor:pointer;
   width: 62px;
   height: 85px;
   background: url('~@/assets/img/rocket.png') no-repeat;
   z-index: 10;
   background-position: -40px -44px;
 }
</style>