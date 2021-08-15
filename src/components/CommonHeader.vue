<template>
<div>
  <!-- pc端导航 -->
  <header>
      <!-- 导航菜单 -->
      <el-menu mode="horizontal" 
      :default-active="activeIndex" 
      @select="handleSelect"
      text-color="#9d9d9d"
      active-text-color="#409EFF"
      class="nav"
      >
        <el-row type="flex" justify="space-around">
          <el-col :span="1">
              <el-menu-item index="1" @click="goToto">
                 <router-link to="/" ><i class="iconfont My-new-iconshouye"></i>博客首页</router-link>
              </el-menu-item>
          </el-col>
          <el-col :span="1">
              <el-menu-item index="2" @click="goToto">
                 <router-link to="/Lists"><i class="iconfont My-new-iconzixun"></i>技术博文</router-link>
              </el-menu-item>
          </el-col>
          <el-col :span="1">
              <el-menu-item index="3" @click="goToto">
                  <router-link to="/timeLocus" ><i class="iconfont My-new-icondaojishi"></i>时间轨迹</router-link>
              </el-menu-item>
          </el-col>
          <el-col :span="1">
              <el-menu-item index="4" @click="goToto">
                 <router-link to="/recommend" ><i class="iconfont My-new-icondianzan"></i>博客推荐</router-link>
              </el-menu-item>
          </el-col>
          <el-col :span="4">
          </el-col>
          <el-col :span="9">
            <el-input placeholder="请输入内容" class="input-with-select">
              <el-button slot="append" icon="el-icon-search"></el-button>
            </el-input>
          </el-col>
          <el-col :span="4">
          </el-col>
          <el-col :span="1" v-if="isSignIn === 0">
              <el-menu-item index="8" @click="goToto">
                 <router-link to="/login"   class="login"><i class="iconfont My-new-iconxuanzhonghaoyou"></i>登录</router-link>
              </el-menu-item>
          </el-col>
          <el-col :span="1" v-else >
              <el-menu-item index="9"  @click="goToto">
                <router-link to="/personal" class="login">
                  <el-popover
                    placement="bottom"
                    title=""
                    width="200"
                    trigger="hover"
                    :visible-arrow="false">
                    <hover :userInfo="UserInfo"></hover>
                    <img :src="head_img" alt="" class="head_img" @mouseenter="showPersonal" slot="reference">
                  </el-popover>
                </router-link>
            </el-menu-item>
          </el-col>
          <el-col :span="1" v-if="isSignIn === 1 && nickname === '小果同学'">
              <el-menu-item index="7"  @click="goToto">
                 <router-link to="/article">我的博客</router-link>
              </el-menu-item>
          </el-col>
          <el-col :span="1" v-else>
              <el-menu-item index="7"  @click="goToto">
                 <router-link to="/article">个人中心</router-link>
              </el-menu-item>
          </el-col>                    
          <el-col :span="1">
              <el-menu-item index="6" @click="goToto">
                 <router-link to="/LeaveWord"><i class="iconfont My-new-iconbianji"></i>留言</router-link>
              </el-menu-item>
          </el-col>          
        </el-row>
      </el-menu>
  </header>
  <div id="mobileNav">
    <!-- 移动端导航 -->
      <el-row class="tac">
      <el-menu
          default-active="2"
          class="el-menu-vertical-demo"
          @open="handleOpen"
          @close="handleClose"
          background-color="#545c64"
          text-color="#fff"
          active-text-color="#ffd04b"
          :router="true">
          <el-submenu index="1">
            <template slot="title">
              <i class="el-icon-location"></i>
              <span class="logotit">风掠的小窝</span>
              <span v-if="UserInfo.nickname">{{UserInfo.nickname}},欢迎您</span>
            </template>
            <el-menu-item-group>
              <el-menu-item index="/" @click="Goto"><i class="iconfont My-new-iconshouye"></i>博客首页</el-menu-item>
              <el-menu-item index="/Lists" @click="Goto"><i class="iconfont My-new-iconzixun"></i>技术博文</el-menu-item>
               <el-menu-item index="/timeLocus" @click="Goto"><i class="iconfont My-new-icondaojishi"></i>ACG</el-menu-item>
              <el-menu-item index="/recommend" @click="Goto"><i class="iconfont My-new-icondianzan"></i>博客推荐</el-menu-item>
              <el-menu-item index="/aboutMe" @click="Goto"><i class="iconfont My-new-iconwode1"></i>关于我</el-menu-item>
               <el-menu-item  index="/LeaveWord" @click="Goto"><i class="iconfont My-new-iconbianji"></i>留言</el-menu-item>
              <el-menu-item index="/personal" v-if="UserInfo.nickname" @click="Goto"><i class="iconfont My-new-iconwode1"></i>{{UserInfo.nickname}}的个人中心</el-menu-item>
              <el-menu-item  index="/login" v-else @click="Goto">登录</el-menu-item>
            </el-menu-item-group>
          </el-submenu>
        </el-menu>
      </el-row>
  </div>
  
</div>
    
</template>
<script>
import Hover from '@/views/Hover'
  export default {
    data() {
      return {
        activeIndex:'1',
        UserInfo:{},
        head_img:'',
        nickname:''
      }
    },
    components:{
      Hover
    },
    methods: {
      // 修改当前活跃
        handleSelect(index) {
          this.activeIndex = index + ''
          window.sessionStorage.setItem('index',this.activeIndex)
        },

      goToto(){
        //console.log(11);
        this.$emit('goTo')
      },
      showPersonal(){
        console.log("111111111")
      },
      
      // 获取用户信息
    async GetInfo(){
        const { data : res }= await this.$http.get('/api/users/info')
        this.UserInfo = res.data
        this.nickname = res.data.nickname
        let avatar = res.data.head_img
        this.head_img = res.data.head_img
        //  获取用户昵称保存在 sessionStorage
        sessionStorage.setItem("avatar", avatar);
        sessionStorage.setItem("nickname", this.nickname);        
        console.log(res)
      },
      // 移动端导航
      handleOpen(key, keyPath,index) {
        console.log(key, keyPath);
        console.log(index);
      },
      handleClose(key, keyPath,index) {
        console.log(key, keyPath);
        console.log(index);
      },
      Goto(){
        let but = document.querySelector('.el-submenu__title');
        but.click();
      }
    },
    computed:{
      isSignIn(){
        return this.$store.state.isSignIn;
      }
    },
    created(){
      this.GetInfo();
      this.activeIndex = window.sessionStorage.getItem('index')
    }

  }
</script>

<style lang="scss" scoped>
header {
  background-image: url(~@/assets/img/nav.png);
  height: 150px;
  .logo {
  font-size: 18px;
  color: #fff;
  text-align: center;
  line-height: 60px;
  }
  .nav {
    background-color: rgba(255, 255, 255, 0);
    li {
      padding: 0;
    }
    a {
      padding: 20px;
      color:#fff;
      .iconfont {
        color: #fff;
        // 垂直居中
        vertical-align: top;
        margin: 0 5px 0 0 ;
      }
    }
    .el-input {
      padding: 10px;
      color:#fff;
    }    
    .login {
      color: #fff;
    }
  }
}

i {
  margin-right: 8px;
}


.el-menu.el-menu--horizontal {
   border-bottom: 0
}
.el-menu-item:hover{
  background-color: rgba(255, 255, 255, 0)!important;
  color: #fff!important;
}
.head_img{
  width: 40px;
  height: 40px;
  border-radius: 50%;
}
</style>