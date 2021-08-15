<template>
  <div>
    <div id="frozen-btn">
      <ul>
          <li class="green"  :key="index"  @click="handle(item.id)"  v-for="(item,index) in data"><span :class="ClassArray[index]">{{index + 1}}</span><span class="item_title">{{item.title}}</span></li>
      </ul>
    </div>
  </div>
</template>

<script>
  export default {
    inject: ['reload'],
    props:['title'],
    data() {
      return {
        data:[],
        ClassArray:['blue','blue','blue','white','white','white','white','white','white','white']
      }
    },
    methods:{
      handle(id) {
        this.$router.replace({name:'detail',params: {id:id}})
        this.reload()
      },
      selectRender(){
        switch(this.title) {
          case '最新推荐' :
            this.data = this.$store.state.RecommendArry
            break
          case '点赞排行' :
            this.data = this.$store.state.LikeArry
            break
        }
      }
    },
    created(){
      // 刷新后重新获取数据
      this.selectRender();
      // 首次进入页面要等到获取文章数据后才能得到排名数据
      this.$EventBus.$on('Render',() => {
        this.selectRender();
      })
      
    }
  }
</script>

<style lang="scss" scoped>

</style>