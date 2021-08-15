<template>
  <div class="personalDetails" id="introduction">
     <!-- 个人简介 -->
             <div class="block">
               <img src="@/assets/img/userinfo.webp" alt="">
               <div class="head_img">
                 <img src="@/assets/img/head.gif" alt="" class="bian">
               </div>               
              <div>
                <div class="content">
                  <div>
                    二次元の前端
                  </div>
                  <div class="user-card-info">
                    <a href="">
                      <p class="num">{{article_num}}</p>
                      <p>文章</p>
                    </a>
                    <a href="">
                      <p class="num">{{essay}}</p>
                      <p>随笔</p>
                    </a>
                    <a href="">
                      <p class="num">{{comment}}</p>
                      <p>留言</p>
                    </a>                                       
                  </div>
                </div>
                <ul class="buttonBox">
                  <li class="item">
                    <a href="https://github.com/uztg" title="github" class="item-wx" target="_blank"></a>
                  </li>
                   <li class="item">
                    <a href="https://space.bilibili.com/2424026" title="B站" class="item-e-mail" target="_blank"></a>
                  </li>
                </ul>
              </div>
            </div> 
  </div>
</template>

<script>
  export default {
    inject: ['reload'],
    data(){
      return {
        // 评论总数
        comment:0,
        // 文章总数（包含 随笔 和技术文）
        article_num:0,
        // 随笔
        essay:0
      }
    },
    methods:{
    async getComments(){
      // 获取留言条数
      const {data : res}  = await this.$http.get('/api/comment/list',{params:{article_id:0}})
      this.comment = res.data.length
      // 获取总文章数目
      const {data : res_num } = await this.$http.get('/api/article/typeList')
      this.article_num = res_num.data.length
      console.log(res_num)

      },
    },
    created(){
      this.getComments()
      //console.log(this.$store.state)
      const essay = this.$store.state.RecommendArry.length
      this.essay = essay
    },
  }
</script>

<style lang="scss" scoped>
 // 个人简介
    .block {
      position: relative;
      height: 100%;
      background-color: rgb(255, 255, 255);
      img{
        width: 100%;
        border-top-left-radius:6px;
        border-top-right-radius:6px;
      }
      .head_img {
        position: absolute;
        left: 50%;
        transform: translateX(-50%);
        margin-top: -52px;
        img {
          width: 100px;
          height: 100px;
          border-radius: 50%;
          border: rgba(255,255,255,.4) 4px solid;
          transition:1s;
          &:hover{
            width: 110px;
            height: 110px;
            transform: rotate(360deg);
          }
        }
      }
    }

.buttonBox {
  display: flex;
  margin: 20px 0 ;
  .item {
    margin: 0 5px;
    cursor:pointer;
    position: relative;
    a {
      display: inline-block;
      width: 50px;
      height: 50px;
      border-radius: 50%;
      background-color: aliceblue;
    }
    .item-e-mail {
      background: url('~@/assets/img/bilibilil.png') no-repeat;
      background-position: 9px 9px;
      background-size: 65%;
      background-color: #fff;
    }
    .item-wx {
      background: url('~@/assets/img/GitHub.png') no-repeat;
      background-position: 5px 5px;
      background-size: 80%;
      background-color: #fff;
    }

  }
}
.iconfont {
  margin-right: 5px;
}
.block{
  color: #000;
}
.content{
margin-top: 50px;
margin-left: 100px;
  .user-card-info{
    margin-left: -100px;
    display: flex;
    justify-content: space-around;
    a{
    width: 33.3%;
    height: 92px;
    text-align: center;
    cursor: pointer;
    }
    p{
      margin-top: 20px;
    }
  }
  .user-card-info .num{
    letter-spacing: 0;
    padding-top: 35px;
    font-weight: 700;
    font-size: 14px;
    color: #00a1d6;
  }
}
</style>