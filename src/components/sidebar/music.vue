<template>
  <div id="music">
    <!-- 搜索框 -->
     <div class="search bar7">
        <div>
            <el-input type="text" placeholder="请输入歌名" name="crid" @keyup.enter.native="playMusic(songName)" v-model="songName"></el-input>
            <el-button slot="append" icon="el-icon-search" type="submit" id="searchMusic" @click="playMusic(songName)"></el-button>
        </div>
    </div>
     <a-player
      :audio="audio"  
      :lrcType="1"
      v-if="flag"
      autoplay
      :listMaxHeight=350
      ref="aplayer"
      ></a-player>
  </div>
</template>

<script>
import {GetSong,GetPlayMisicUrl,GetPlayMisicLyric} from "@/musicNetWork/music.js"; 
  export default {
    data() {
      return {
        songName:'泠鸢yousa',
        flag:false,
         // 音频列表
        audio:[],
      }
    },
    methods: {
      playMusic(songName){
        if(!songName) return songName = this.songName
        this.songName = ''
        // 定义一个存放歌词数据对象的数组
        let songDataArray = []
        GetSong(songName).then(res => {
           //console.log(res.result.songs);
          // 循环请求得到的歌曲数据
          res.result.songs.forEach( async (item,index,array) => {
            // 定义一个对象，用于存放具体数据
            let songData = {}
            // 获取歌名
            songData.name = item.name
            // 获取歌手名
            songData.artist = item.ar[0].name
            // 获取照片
            for(var key in  item.al){
              songData.cover = item.al.picUrl + '?param=100y100'
            }
            // 获取歌曲播放地址
            let musicUrl = await GetPlayMisicUrl(item.id)
            songData.url = musicUrl.data[0].url            
            // 获取歌词
            let MisicLyric = await GetPlayMisicLyric(item.id)
            if(MisicLyric.nolyric){
              songData.lrc = '[00:00.00] (,,•́ . •̀,,) 抱歉，当前歌曲暂无歌词'
            }else {
              songData.lrc = MisicLyric.lrc.lyric
              
            }
            //  完成此条数据的循环，将得到的歌曲数据push到数组
             songDataArray.push(songData)
    　　　  }
　　       );
        })
        // 将此次搜索得到的数据全部赋值给audio,等待播放
        this.audio = songDataArray
        this.flag = true
      },
    },
    mounted(){
      // 页面刷新添加一个自动点击事件
      let searchMusic = document.querySelector('#searchMusic');
        searchMusic.click();

    },
  }
</script>

<style lang="scss" scoped>
* {
	box-sizing:border-box;
}
// 音乐组件
.aplayer {
  margin: 0;
  margin-top: 15px;
  border-radius: 5px;
}
#container {
	width:500px;
	height:820px;
	margin:0 auto;
}
div.search {
	padding:10px 0;
  transform: translateY(20px);
}
div {
	position:relative;
	margin:0 auto;
}
input,button {
	border:none;
	outline:none;
}
input {
	width:100%;
	height:42px;
	padding-left:13px;
}
button {
	height:42px;
	width:42px;
	cursor:pointer;
	position:absolute;
}
/*搜索框7*/
      
.bar7 div {
	height:42px;
}
.bar7 input {
	width:250px;
	border-radius:42px;
	border:2px solid #324B4E;
	background:#F9F0DA;
	transition:.3s linear;
	float:right;
}
.bar7 input:focus {
	width:300px;
}
.bar7 button {
	background:none;
	top:-2px;
	right:20px;
}
.bar7 button:before {
	content:"";
	font-family:FontAwesome;
	color:#324b4e;
}
</style>