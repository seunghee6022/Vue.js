<template>
  <div class="list-group">
      
      <VideoListItem v-for="video in videos" 
      :key="video.etag"
      :video="video"
      @send-to-detail="sendToDetail"
      />
   

  </div>
</template>

<script>
import VideoListItem from './VideoListItem.vue'

export default {
    name: 'VideoList',
    components: {
        VideoListItem,
    },

    props : {
        videos : Array,
       
    },
    methods : {
      sendToDetail(video) {
        console.log("VideoList", video.snippet.title)
        this.$emit('send-to-detail',video)
      }
    }
}
</script>

<style>

</style>