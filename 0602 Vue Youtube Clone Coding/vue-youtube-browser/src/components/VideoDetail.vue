<template>
  <div v-if="video" class="col-lg-8 p-3">
      <div class="video-detail">
          <div class="embed-responsive embed-responsive-16by9">
            <iframe 
            class="embed-responsive-item" 
            :src="videoUrl"
            allowfullscreen>
            </iframe>
        </div>
        <div class="details p-2 list-group-item mt-3">
           <h4>{{video.snippet.title}}</h4> 
           <p>{{video.snippet.description}}</p>
        </div>
        
      </div>
  </div>
</template>

<script>
export default {
    name : 'VideoDetail',
    props : {
        video : Object,
    },
    computed : {
        videoUrl() {
            return `https://www.youtube.com/embed/${this.video.id.videoId}`
        }
    },
    methods : {
       
    }
}

    
</script>

<style>

</style>