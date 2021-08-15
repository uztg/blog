<template>
  <div class="commonLayout">
    <!-- 导航条 -->
    <nav>
      <common-header @goTo="goTo()" class="wow slideInRight" style="top:0px"></common-header>
    </nav>

    <!-- 切换大屏阅读模式按钮 -->
    <!-- <check-box isname="read"></check-box> -->

      <!-- 中心 -->
      <section>
        <div class="wrapper marginTop">
            <el-row :gutter="10" class="head" v-show="!isShowDiv">
              <el-col :lg="6" :xl="6">
                <div class="grid-content bg-purple-light synopsis" ref="sidebar">
                  <!-- 侧边栏 -->
                    <aside class="wow slideInRight">
                      <personal-details class="wow slideInRight"></personal-details>
                      <music class="maginbot wow slideInLeft" data-wow-delay="0.2s"></music>
                    </aside>
                </div>
              </el-col>
              <el-col :xs="24" :sm="24" :md="24" :lg="12" :xl="12">
                <div class="grid-content bg-purple slideshowBox">
                  <!-- 视图切换 -->
                    <article ref="article">
                      <keep-alive include="timeLocus">
                        <router-view></router-view>
                      </keep-alive>
                    </article>
                </div>
                </el-col>
              <el-col :lg="6" :xl="6">
                <div class="">  
                  <tally class="maginbot"></tally>
                  <!-- <div class="block maginbot">
                    <h4>最新推荐</h4>
                    <ranking-list title="最新推荐"></ranking-list>
                  </div> -->
                  <div class="block maginbot">
                    <h4>排行榜</h4>
                    <ranking-list title="点赞排行"></ranking-list>
                  </div>            
                </div>
                </el-col>                
            </el-row>
            <!-- 动画效果展示  -->
            <animation  v-if="isShowDiv"></animation>
        </div>
        
      </section>

    <!-- 底部 -->
    <footer>
      <common-bottom v-if="isFooterShow"></common-bottom>
    </footer>
  </div>
</template>

<script>
import CommonHeader from '@/components/CommonHeader.vue'
import CommonBottom from './CommonBottom.vue'
import PersonalDetails from './sidebar/personalDetails.vue'
import Music from './sidebar/music.vue'
import Tally from './sidebar/tally.vue'
import RankingList from './sidebar/rankingList.vue'
import CheckBox from '@/components/checkbox/checkbox.vue'
import Animation from '../views/animation.vue'
export default {
  name: 'commonLayout',
  components:{
    CommonHeader,
    CommonBottom,
    PersonalDetails,
    Music,
    Tally,
    RankingList,
    CheckBox,
    Animation
  },
  data() {
    return {
      isShowDiv:false,
      isFooterShow:false
    }
  },
  methods: {
    goTo(){
      this.isShowDiv = false
    },

  },
  created(){
    // this.$nextTick(()=>{
    //   this.isFooterShow = true
    // })
    setTimeout(()=>{
      this.isFooterShow = true
    },1000)
  }
 
}
</script>

<style scoped lang="scss">
.commonLayout {
  // width: 100%;
  // height: 100%;
  // 导航条
    .common-header {
    position: fixed;
    top: 0;
    right: 0;
    left: 0;
    z-index: 999;
  }
  // 切换部分
  section {
    .slideshowBox {
       margin-right: 7px;
    }   
  }
  // 侧边栏
  aside {
    width: 100%;
    .maginbot {
      margin-bottom: 20px;
      width: 100%;
    }
  }
  .block{
    margin-top: 10px;
  }
  h4{
    padding: 10px;
    font-weight: bold;
    border-bottom: 1px solid #e7e7e7;    
  }
}


</style>
