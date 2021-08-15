<template>
  <div class="hover_info">
      <span>{{userInfo.nickname}}</span>
  </div>
</template>

<script>
export default {
  props:{
    userInfo:{}
  }
}
</script>

<style>
.hover_info{
  color: #Fb7299;
  text-align: center;
}
</style>