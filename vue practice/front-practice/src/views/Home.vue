<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HomeComp1/>
  </div>
</template>

<script>
// @ is an alias to /src
import HomeComp1 from '@/components/HomeComp1.vue'

export default {
  name: 'Home',
  components: {
    HomeComp1
  }
}
</script>
