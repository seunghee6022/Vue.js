# 0527 Vue Router Cli Workshop

### Code

* App.vue

```vue
<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Index</router-link> |
      <router-link to="/lotto">Lotto</router-link> |
      <router-link to="/lunch">Lunch</router-link> |
      <router-link to="/cat">Cat</router-link>
    </div>
    <router-view/>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>

```

* Index.vue

```vue
<template>
  <div>
   <p>사용 가능한 기능</p>
   <p>메뉴추천, 로또번호생성</p>
    
  </div>
</template>

<script>

export default {
  name: 'Index',
  
}
</script>

```



* Lotto.vue

```vue
<template>
<div>
  <h1>Lotto</h1>
  <button @click="getNums">숫자생성</button>
  <p>{{lucky}}</p>
</div>
</template>

<script>
import _ from 'lodash'

export default {
  name : 'Lotto',
  data : function (){
    return {
      lucky : '',
      nums : _.range(1,46)
    }
  },
  methods : {
    getNums : function () {
      this.lucky = _.sampleSize(this.nums, 6)
    }
  }
}
</script>

<style>

</style>


```



* Lunch.vue

```vue
<template>
  <div>
      <h1>Lunch</h1>
      <p>{{menus.join(', ')}}</p>
      <button @click="pickMenu">랜덤선택</button>
      <p>{{pick}}</p>
  </div>
</template>

<script>
import _ from 'lodash'

export default {
    name : "Lunch",
    data : function () {
        return {
            pick : '',
            menus : [
                '짜장',
                '짬뽕',
                '김밥',
                '라면',
                '초밥',
                '회',
                '돈가스'
            ]

        }
    },
    methods: {
        pickMenu() {
            this.pick = _.sample(this.menus)
        }
    }
}
</script>

<style>

</style>
```

* Cat.vue

```vue
<template>
<div>
<h1>Cat</h1>
  <button @click='getCatImg'>야옹</button>
  <div>
      <img :src="imgUrl" alt="img" v-show="imgUrl !== ''">
  </div>

</div>
  
</template>

<script>
import axios from 'axios'

export default {
    name : 'Cat',

    data : function () {
        return {
            imgUrl:'',
        }
    },
    methods : {
        getCatImg : function () {
            const catUrl = 'https://api.thecatapi.com/v1/images/search'
            axios.get(catUrl)
            .then(res =>{
                console.log(res)
                this.imgUrl = res.data[0].url
            })
            .catch(err =>{
                console.error(err)
            })
            
        }
}
}
</script>

<style>
    img {
        height:300px;
    }
</style>
```



* index.js

```js
import Vue from 'vue'
import VueRouter from 'vue-router'
import Index from '../views/Index.vue'
import Lotto from '../views/Lotto.vue'
import Lunch from '../views/Lunch.vue'
import Cat from '../views/Cat.vue'


Vue.use(VueRouter)

  const routes = [
  {path: '/', name: 'Index', component: Index},
  {path: '/lotto', name: 'Lotto', component: Lotto},
  {path: '/lunch', name: 'Lunch', component: Lunch},
  {path: '/cat', name: 'Cat', component: Cat},
]

const router = new VueRouter({
  mode: 'history',
  base: process.env.BASE_URL,
  routes
})

export default router

```



---

### 결과 사진

* index

![](C:\Users\tgb03\Desktop\online-lecture\0527\workshop\index.PNG)

* lotto

![](C:\Users\tgb03\Desktop\online-lecture\0527\workshop\lotto.PNG)

* lunch

![](C:\Users\tgb03\Desktop\online-lecture\0527\workshop\lunch.PNG)

* cat

![](C:\Users\tgb03\Desktop\online-lecture\0527\workshop\cat.PNG)