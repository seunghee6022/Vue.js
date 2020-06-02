# 0601 Vue Youtube Workshop

* App.vue

```vue
<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <SearchBar @result='addResult'/>
    
    <Detail/>
    <List :items="items"/>
  
    </div>
</template>

<script>
import SearchBar from './components/SearchBar.vue'
import Detail from './components/Detail.vue'
import List from './components/List.vue'

export default {
  name: 'App',
  components: {
    SearchBar,
    Detail,
    List 
  },
  data () {
    return {
      items : [

      ]
    }
  },
  methods : {
    addResult (items) {
      this.items = items
      console.log(this.items)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

</style>

```

* List.vue

```vue
<template>
  <div>
      <h1>Video List</h1>
      <ul>
          <li v-for="item in items" :key="item.etag">
              {{item.snippet.title}}
          </li>
      </ul>
  </div>
</template>

<script>
export default {
name: 'List',

props: {
    items : Array,
}
}
</script>

<style>

</style>
```

* SearchBar.vue

```vue
<template>
  <div>
      <!-- v-model 쓰는 이유: 여기 vue파일에서만 사용할 것이므로 -->
      <input type="text" v-model='search' >
      <button @click="searchVideo(search)">검색</button>
  </div>
</template>

<script>
import axios from 'axios'

const API_KEY = 'AIzaSyDDufc_3Sjg-i3_4C69Q0Uj-SbW3iFTFVE'
const API_URL = 'https://www.googleapis.com/youtube/v3/search'

export default {
name : "SearchBar",
    
data () {
    return{
        search :'',
    }
},
methods: {
    searchVideo (search) {
        this.search = search
        axios.get(API_URL,{
            params:{
                key:API_KEY,
            part : 'snippet',
            type : 'video',
            q : this.search,
            }
        })
       .then(res =>{
           console.log(res.data.items)
           this.$emit('result',res.data.items)
       })
       .catch(err => console.error(err))
    }
}
}
</script>

<style>

</style>
```

