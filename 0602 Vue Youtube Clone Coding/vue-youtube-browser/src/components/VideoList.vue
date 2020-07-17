<template>
  <div>
      This is VideoList
      <br>
      <!-- <v-for :key="video.etag" -->
      {{videos}}
  </div>
</template>

<script>
export default {
    name: 'VideoList',

    props : {
        videos : Array,
    }
}
</script>

<style>

</style>