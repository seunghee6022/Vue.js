<template>
  <div class="container text-center">
    <h2 class="red">Youtube Clone Coding</h2>
    <SearchBar class="red" @event-submit="onInputText"/>
    <div class="row">
       <VideoDetail :video='selectedVideo'/>
       <VideoList :videos='videos' @send-to-detail="onVideoClick"/>  
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import SearchBar from '@/components/SearchBar.vue'
import VideoList from '@/components/VideoList.vue'
import VideoDetail from '@/components/VideoDetail.vue'
/* 
.env.local 파일에 작성한 변수명이 서버 최초 실행시에
process.env.변수명으로 자동 설정된다.
단, 변수명의 접두사가 VUE_APP_이어야 한다.!!!!
*/
const API_URL = 'https://www.googleapis.com/youtube/v3/search'
const API_KEY =  process.env.VUE_APP_YOUTUBE_API_KEY


export default {
  name : 'App',
  components :{
    SearchBar,
    VideoList,
    VideoDetail,
  },
  data() {
    return {
      inputValue : '',
      videos : {},
      selectedVideo : {},
    }
  },
 
  methods: {
   
    onInputText(inputText) {
      this.inputValue = inputText
      console.log(API_KEY)

      axios.get(API_URL, {
        params: {
          q : this.inputValue,
          key : API_KEY,
          part : 'snippet',
          type : 'video',
        }
      })
      .then(res=>{
        console.log(res.data)
        this.videos = res.data.items
      
      })
      .catch(err=>console.log(err))
    },

     onVideoClick(video) {
       this.selectedVideo = video
     }
  
  }
}
</script>

<style>
  .black {
    border : 2px solid lightgray;
    /* text-align : center; */
  }
  .red {
    /* border :2px solid red; */
    padding : 5px;
  }
  .blue {
    border : 2px solid gray;
  }
  .green {
    border : 2px solid green;
  }
 
</style>