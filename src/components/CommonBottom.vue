<template>
  <div id="mybottom" class="bottom">
    <!-- 计时器 -->
    <timer class="timer"></timer>
    <div class="conent">
      <p>
        <span>
          <a href="http://hzfe-xg.com:36543/#/">风掠的小窝</a>
        </span>
      </p>
      <p>
        <span>
          
        </span>
      </p>
    </div>
  </div>
</template>

<script>
import timer from './timer.vue'
  export default {
  components: { timer },
    methods:{

    }
  }
</script>

<style lang="scss" scoped>
.bottom {
  margin-top: 30px;
  width: 100%;
  background-color: #373D41;
  position: relative;
  .timer {
    position: absolute;
    right: 15px;
    color: #73777a;
    bottom: 15px;
    font-size: 14px!important;
  }
  .conent {
    margin-top: 10px;
    color: #73777a;
    font-size: 14px;
    display: flex;
    justify-content: flex-start;
    line-height: 50px;
     p {
      margin-top: 5px;
      text-align: center;
      span {
          line-height: 30px;
      }
    }
  }
}
</style>