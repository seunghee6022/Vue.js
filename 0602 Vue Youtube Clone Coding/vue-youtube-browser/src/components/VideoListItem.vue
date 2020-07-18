<template>
  <div class="list-group-item" @click="onSubmit">
      <p>{{video.snippet.title}}</p>
       
  </div>
</template>

<script>
export default {
    name:'VideoListItem',
    props : {
        video : Object,
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

</style>