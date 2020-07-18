<template>
  <div class="list-group-item d-flex mouse" @click="onSubmit">
      <img :src="thumbnailUrl">
      <p>{{video.snippet.title}}</p>
       
  </div>
</template>

<script>
export default {
    name:'VideoListItem',
    props : {
        video : Object,
    },
    // 함수지만 명사형 => 결국 리턴되는 값이 사용되기 때문.
    computed : {
        thumbnailUrl() {
            return this.video.snippet.thumbnails.default.url
        }
    },
    methods : {
        onSubmit() {
            console.log(this.video.snippet.title)
            this.$emit('send-to-detail',this.video)
        }
    }
}
</script>

<style>
.mouse:hover{
    background-color : lightgray;
}
</style>