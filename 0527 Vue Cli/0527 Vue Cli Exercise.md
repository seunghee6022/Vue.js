# Vue Cli

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
$create create 프로젝트이름

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

---

### 결과사진

* index

![](C:\Users\tgb03\Desktop\online-lecture\0527\exercise\index.PNG)

* lotto

![](C:\Users\tgb03\Desktop\online-lecture\0527\exercise\lotto.PNG)

* lunch

![](C:\Users\tgb03\Desktop\online-lecture\0527\exercise\lunch.PNG)