<template>
  <div class="container">
      This is VideoList
      <br>
      <VideoListItem v-for="video in videos" 
      :key="video.etag"
      :video="video"
      />
    {{videos}}

  </div>
</template>

<script>
import VideoListItem from './VideoListItem.vue'

export default {
    name: 'VideoList',
    conponents: {
        VideoListItem,
    },

    props : {
        videos : Array,
    }
}
</script>

<style>

</style>