# 0602 YouTube Clone Workshop

* App.vue

```vue
<template>
  <div id="app" class="container">
    <img alt="Vue logo" src="./assets/logo.png">
    <SearchBar @result='addResult'/>
    <div class="row">
       <Detail :video="selectedVideo"/>
    <List :items="items" @video-select="onVideoClick"/>
  
    </div>
   
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
      items : [],
      selectedVideo : null,
    }
  },
  methods : {
    addResult (items) {
      this.items = items
      console.log(this.items)
    },
    onVideoClick(video){
      console.log("APP:",video.snippet.title)
      this.selectedVideo = video
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

* SearchBar.vue

```vue
<template>
  <div>
      <!-- v-model 쓰는 이유: 여기 vue파일에서만 사용할 것이므로 -->
      <input type="text" v-model='search' class="w-75 mb-3" @keypress.enter="searchVideo(search)">
      <button @click="searchVideo(search)">검색</button>
  </div>
</template>

<script>
import axios from 'axios'

const API_KEY = process.env.VUE_YOUTUBE_API_KEY
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
           res.data.items.forEach(item=>{
               const parser = new DOMParser()
               const doc = parser.parseFromString(item.snippet.title, 'text/html')
               item.snippet.title = doc.body.innerText
           })
        //    this.videos = res.data.items
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

* List.vue

```vue
<template>
  <!-- <div> -->
      <div class="list-group col-lg-4">
        <!-- <h1>Video List</h1> -->

        <VideoListItem v-for="item in items" 
        :key="item.etag" 
        :item="item" 
        @video-select="onVideoClick"
        />
      </div>
  <!-- </div> -->
</template>

<script>
import VideoListItem from './VideoListItem.vue'
export default {
name: 'List',
components :{
    VideoListItem,
},
props: {
    items : Array,
  
},
methods : {
    onVideoClick(item){
        console.log("VL",item.snippet.title)
        this.$emit('video-select',item)
    }
}
}
</script>

<style>

</style>
```

* Detail.vue

```vue
<template>
<div v-if="video" class="col-lg-8">
  <div class="embed-responsive embed-responsive-16by9">
    <iframe class="embed-responsive-item" 
    :src="videoUrl" 
    allowfullscreen>
    </iframe>

</div>
  <div class="details">
    <!-- innerHTML : 보안상의 이유로 쓰면 안됀다. -->
    <!-- <h4 v-html="video.snippet.title"></h4> -->
    <!-- innerText -->
      <h4>{{video.snippet.title}}</h4>
      <p>{{video.snippet.description}}</p>
     
  </div>
  </div>
</template>

<script>

export default {
name : "Detail",

props:{
    video : Object,
  },
computed : {
    videoUrl () {
      return `https://youtube.com/embed/${this.video.id.videoId}`
    }
  },

}
</script>

<style>
div.details {
  margin-top : 10px;
  padding : 10px;
  border : 1px solid #dddddd;
  border-radius: 4px;
}
</style>
```



