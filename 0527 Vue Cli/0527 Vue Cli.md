# router-linkVue Cli

### Vue의 component = Vue instance (미리 정의된 옵션을 가진 Vue 인스턴스)

> 왜? 관리하기 쉬워서, 재사용성을 위해서 => 쉬운관리 & 재사용성



### Vue에서의 Component관리

__파일관리 (.vue) =>  Single File Component (SFC)__ : 컴포넌트를 파일로써 관리



> 인스턴스로 관리 가능 (JS + HTML) => 코드가 길어지고 관리가 불편하기떄문에 파일로 관리

```js
Vue.component( 'todo-item', {
    ...
})
```

```html
연결위해 코드 추가해야함
```



> 파일관리 (.vue)



### 명령어

```bash
프로젝트 생성하기
$vue create 프로젝트이름
$cd 플젝이름
$vue add router -> history (Y)

서버 실행
$npm run serve
```



### lodash : 랜덤숫자 추첨위해 깔아야함

```
//터미널에서
$npm i --save lodash
```

```vue
//<script>밑에
import _ from 'lodash'
```



----

### 0527 Lotto, Lunchmenu, Index Exercise

* App.vue

```vue
<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  <div>
    <button @click='setIndex'>Index</button>
    <button @click='setLotto'>Lotto</button>
    <button @click='setLunch'>Lunch</button>
  </div>
    <Index v-if="status === 'index'"/>
    <Lotto v-else-if="status === 'lotto'"/>
    <LunchMenu v-else/>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import Index from './components/Index.vue'
import Lotto from './components/Lotto.vue'
import LunchMenu from './components/LunchMenu.vue'


export default {
  name: 'App',
  components: {
    Index,
    Lotto,
    LunchMenu,
  },
 data : function () {
   return {
     status : 'index',

   }
 },
 methods: {
   setIndex : function () {
     this.status = 'index'
   },
   setLotto : function () {
     this.status = 'lotto'
   },
   setLunch : function () {
     this.status = 'lunch'
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

* Index.vue

```vue
<template>
<div>
    <!-- 템플릿 태그 안엔 하나의 요소만 있어야 하므로 div안에 모두 넣는다. -->

  <p>사용 가능한 기능</p>
   <p>메뉴 추천, 로또번호 생성</p>
  
</div>
</template>

<script>
export default {
  //data는 함수여야만 한다.
  data : function () {
    return {
    

    }
  },

  

}
</script>

<style>

</style>
```

* Lotto.vue

```vue
<template>
  <div>
      <h1>Lotto</h1>
     <button @click="getLottoNums">숫자 생성</button> 
     <p>{{lottoNums}}!!!!</p>
  </div>
</template>

<script>
import _ from 'lodash'

export default {
    data : function () {
        return {
            numbers : _.range(1,46),
            lottoNums : '당장 토욜에 달려갈 번호는?!?!?!?!?',
        }

    },
    methods : {
        getLottoNums : function () {
            this.lottoNums = _.sampleSize(this.numbers,6).sort((a,b) => a-b)
        }
    }
}
</script>

<style>

</style>
```

* LunchMenu.vue

```vue
<template>
<div>
   <h1>Lunch</h1>
    <p>{{menus.join(', ')}}</p>
     <button @click="pickLunchMenu">랜덤선택</button> 
     <p>{{lunchMenu}}!!!!</p>
</div>
</template>

<script>
import _ from 'lodash'

export default {
    data : function () {
        return {
        menus : [
            '짜장',
            '짬뽕',
            '김밥',
            '라면',
            '돈가스',
            '초밥',
            '찜닭',
            '파스타',
            '햄버거',
            '회',
            '쌀국수'
        ],
        lunchMenu : '오늘 메뉴는 과연????!?!?!?!',
        }
    },
   
    methods : {
        pickLunchMenu : function () {
            this.lunchMenu = _.sample(this.menus)
        }
    }
}
</script>

<style>

</style>
```

--------

# Live2 - URL에 따른 다른 컴포넌트 렌더링(router)

* router

```ba
$vue add router
```

* router-link : <a>로 렌더링 되지만, 차이점은 새로고침을 걱정하지 않아도 된다. 

```vue
 <router-link to="/">Home</router-link> |
 <router-link to="/about">About</router-link>
```

* 보여줄 페이지들 -> views에 ,  한 페이지의 요소들 -> components
* URL 경로 흐름은 Django와 비슷하다.

> App.vue() -> index.js(path...) ->Home.vue
>
> ![](C:\Users\tgb03\Desktop\Vue.js\0527 Vue Cli\Django 처럼 url 받는 순서 흐름.PNG)

---

### 3 steps for use (1.import-> 2.컴포넌트 등록->3.사용)

```
<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
     <!-- step.3 : 사용 한다. -->
    <MyComponent msg="마이 컴포넌트 등록해보겠습니다."/>
    <GreatComponent/>
  </div>
</template>

<script>
//컴포넌트 사용하기
// step.1 : import 한다.
import HelloWorld from './components/HelloWorld.vue'
import MyComponent from './components/MyComponent.vue'
import GreatComponent from './components/GreatComponent.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    // step.2 : 등록 한다.
    MyComponent,
    GreatComponent,
  }
}
</script>
```

---



 1. App.vue

    ```vue
    <router-link to="/">Home</router-link> |
          <router-link to="/about">About</router-link>
    ```

    

 2. router/ index.js

    > component: 컴포넌트이름 이거 하려면 위에 import 해줘야

    ```js
    import Home from '../views/Home.vue'
    import About from '../views/About.vue'
    
    ```

    

    ```js
     const routes = [
      { path: '/', name: 'Home', component: Home },
      { path: '/about', name: 'About', component:About }
    ]
    ```

	3. views/Home.vue&About.vue

    ```vue
    //Home.vue
    export default {
      name: 'Home',
      components: {
        //2. 등록
        MyComponent,
      }
    
    //About.vue
    <template>
      <div class="about">
        <h1>This is an about page</h1>
      </div>
    </template>
    
    ```

    Home.vue full code

    ```vue
    <template>
      <div class="home">
         <!-- 3. 사용 -->
        <MyComponent/>
         </div>
    </template>
    
    <script>
    // @ is an alias to /src
    // 1. import
    import MyComponent from '@/components/HelloWorld.vue'
    
    export default {
      name: 'Home',
      components: {
        //2. 등록
        MyComponent,
      }
    }
    </script>
    
    ```

	4. Home.vue -> MyComponet.vue

---

### Full code

* App.vue (Router전)

```vue
<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
     <!-- step.3 : 사용 한다. -->
    <MyComponent msg="마이 컴포넌트 등록해보겠습니다."/>
    <GreatComponent/>
  </div>
</template>

<script>
//컴포넌트 사용하기
// step.1 : import 한다.
import HelloWorld from './components/HelloWorld.vue'
import MyComponent from './components/MyComponent.vue'
import GreatComponent from './components/GreatComponent.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    // step.2 : 등록 한다.
    MyComponent,
    GreatComponent,
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

* MyComponent.vue

```vue
<template>
<div>
    <h1>나의 첫 컴포넌트</h1>
    <h1>{{ msg }}</h1>
</div>
</template>

<script>


export default {
  name: 'MyComponent',
  props: {
    msg: String
  }
  
}
</script>

<style>
</style>
```

* CreateComponent.vue

```vue
<template>
<div>
  <h1>안녕하세요 ㅎㅎ</h1>
  <h2>{{message}}</h2>
  <ul>
      <button @click='getPosts'>가즈아</button>
      <li v-for='post in posts' :key='post.id'>
          {{post.content}}
      </li>
  </ul>
  </div>
</template>

<script>
import axios from 'axios'

export default {
    name : 'GreatComponent',
    data : function () {
        return {
            message: 'hi',
            posts : [
                {id:1, title:'hello', content:'hi'},
                {id:2, title:'hi', content:'안녕'},
            ],
        }
    },
    methods : {
        getPosts : function() {
            axios.get('https://koreanjson.com/posts')
            .then(res=> this.posts = res.data)
        },
    },
}
</script>

<style>

</style>
```

---



* App.vue

```vue
<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view/>
  </div>
</template>
<script>
export default {
  
}
</script>
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

* MyComponent.vue

```vue

```



* Home.vue

```vue

```

* About.vue

```vue

```



---

### Export

> JS는 매번 export 해줘야 한다. Django는 모듈이 잘 되어있어서 그냥 import 하면 됐다.

* deport
  * 모듈 하나당 하나의 export만 가능
  * 작명이 자유롭다
* 일반적으로 방법 2개
  * 이름 있이 -  한 file에서 여러개 내보낼 수 있다.
  * 이름 없이

### History

>  url요청했을 때 해당 url기록이 브라우저에 남게된다.
>
> 이 기능이 있으면 뒤로가기, 앞으로가기 등 가능



### Cli

> vue프로젝트 시작할 때, 자동으로 패키지 다 만들어주는것. 없으면 수동으로 해야해서 번거롭다.

* 그냥 vue cli버전과
* vue add router를 한 router cli도 있다.
* @ :  /src

