<template>
  <div>
    Youtube Clone Coding
    <SearchBar @event-submit="onInputText"/>
  </div>
</template>

<script>
import SearchBar from '@/components/SearchBar.vue'
import axios from 'axios'



export default {
  name : 'App',
  components :{
    SearchBar,
  },
  data() {
    return {
      inputValue : '',
    }
  },
  methods: {
    onInputText(inputText) {
      this,inputValue = inputText
      console.log(inputText)

    }
  }
}
</script>

<style>

</style>