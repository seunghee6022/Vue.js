<template>
  <div>
      <input class="w-50" type="text" @keypress.enter="submit">
      <button @click="submit">search</button>
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