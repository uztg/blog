<template>
  <div>
    <div class="block recommend wow slideInRight">
      <h4>优秀博客</h4>
      <div>
        <ul>
          <li :key="index" v-for="(item,index) in ArrayBlog"><a :href="item.url" target="_blank">{{item.name}}</a></li>
        </ul>
      </div>
        <h4>资源导航</h4>
      <div>
        <ul>
          <li :key="index" v-for="(item,index) in ArrayStudy"><a :href="item.url" target="_blank">{{item.name}}</a></li>
        </ul>
      </div>
      <!-- <h4>个人项目集</h4>
      <div>
        <ul>
          <li :key="index" v-for="(item,index) in production"><a :href="item.url" target="_blank">{{item.name}}</a></li>
        </ul>
      </div> -->
      <h4>web前端学习路线</h4>
      <div>
        <ul>
          <li :key="index" v-for="(item,index) in learning"><router-link to="/LearningPath">{{item.name}}</router-link></li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import WOW from 'wowjs';
import titleBox from '../components/TitleBox/titleBox.vue'
  export default {
    name:'recommend',
    components: { titleBox },
    data() {
      return {
        ArrayBlog:[
          {
            name:'阿盖',
            url:'http://xyxiao.cn/'
          },
          {
            name:'夜猫',
            url:'https://nightcat.win/'
          }
        ],
        ArrayStudy:[
          {name:"网道 / WangDoc.com",url:"https://wangdoc.com/javascript/"},
          {name:"阿里图标",url:"https://www.iconfont.cn/"},
          {name:"W3school",url:"https://www.w3school.com.cn/html/index.asp"},
          {name:'在线编码平台 codepen.io',url:"https://codepen.io/"}
          ],
        
        production:[
          {name:'niuniu音乐(线上)',url:'http://bao.lqjhome.cn:13008'},
          {name:'niuniu音乐(Gitee)',url:'https://gitee.com/huang-rijian/vue-net-ease-cloud-music'},
        ],
        learning:[
          {name:'web前端学习路线'}
        ]
      }
    },
    mounted(){
      let wow = new WOW.WOW({
          boxClass: 'wow',
          animateClass: 'animated',
          offset: 0,
          mobile: true,
          live: true
      });
        wow.init();
    }

  }
</script>

<style lang="scss" scoped>
.block{
  padding: 10px;
  h4{
    padding: 10px;
    font-weight: bold;
    border-bottom: 1px solid #e7e7e7;
  }
}
 ul {
   margin-top: 10px;
   display: flex;
   flex-wrap: wrap;
   li {
      margin: 8px 9px;
      border-radius: 5px;
      padding: 10px 17px;
      border: 1px solid rgba(195, 194, 194, 0.5);
      cursor: pointer;
   }
   li:nth-child(n+1):hover {
     background:rgb(230, 54, 54);
     color: white;
   }
   li:nth-child(2n+2):hover {
     background:rgb(198, 230, 54);
     color: white;
   }
   li:nth-child(n+3):hover {
     background:rgb(54, 180, 230);
     color: white;
   }
   li:nth-child(2n+4):hover {
     background:rgb(230, 54, 163);
     color: white;
   }
 }

 .assets {
   margin-top: 20px;
 }
</style>