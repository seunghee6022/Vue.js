<template>
  <ul class="list-group col-lg-4 p-3">
      <VideoListItem v-for="video in videos" 
      :key="video.etag"
      :video="video"
      @send-to-detail="sendToDetail"
      />
  </ul>
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
        console.log("VideoList", video)
        this.$emit('send-to-detail',video)
      }
    }
}
</script>

<style>

</style>