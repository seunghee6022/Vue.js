<template>
  <div>
      SearchBar
      <input type="text" @keypress.enter="submit">
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

</style>