<template>
  <div class="inline">
      <input class="search-bar" type="text" @keypress.enter="submit">
      <button @click="submit" class="btn btn-danger">search</button>
  </div>
</template>

<script>
export default {
    name: 'SearchBar',

    methods: {
        submit(event) {
            console.log(event.target.value)
            this.$emit('event-submit',event.target.value)
        }
    }

    
}
</script>

<style>
.search-bar {
    width: 65%;
}
</style>