# Vue.js _ 1

> JS위한 math pakage library - `lodash` CDN 이용해야

---

### Vue.js

> 1. Front-End-Framework -> Front-End(Client-Side)
>
> 2. SPA( SIngle Page Application) 제작
>
> 3. Client Side Rendering
>
> ![](C:\Users\tgb03\Desktop\Vue.js\0525\캡처.PNG)

​	Client side에서 최종 rendering을 담당하게 되었따.

> ![](C:\Users\tgb03\Desktop\Vue.js\0525\Client Side Rendering2.PNG)
>
> 4. MVVM(Model View ViewModel) 패턴
>
> ![](C:\Users\tgb03\Desktop\Vue.js\0525\MTVVM.PNG)
>
> 5. 반응형 (Reactive)/ 선언형(Declarative)
>
>    한개의 행동에 대해 많은 새로고침들이 필요하다.
>
>    페이스북용 -> React



### MVVM

* Model : object
* View : Html
* ViewModel : 중개자 역할

```html
# app : model, new Vue() : ViewModel역할,  initObj : object역할 => new Vue(initObj) : ViewModel

const app = new Vue(initObj)

var                                                                                                                                                                  
```



 

### Why 쓰는 이유

![](C:\Users\tgb03\Desktop\Vue.js\0525\Why.PNG)



### CDN

```html
<body>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
    </script>
</body>

```



### Vue Tutorial

* el : 

  > Vue에서 정의한 속성 : el. el뒤에 element지정해주면 Vue의 인스턴스와 html에 그 엘리먼트를 연결해줌,
  >
  >  app이라는 id를 가진 html 요소와 연결하겠다.

* data :

  >  MVVM에서 Model. 인스턴스 모든 속성 저장 가능

```html
<body>
    <div id="app">{{message}}</div>
    
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
    var app = new Vue({
        // Vue에서 정의한 속성 : el. el뒤에 element지정해주면 Vue의 인스턴스와 html에 그 엘리먼트를 연결해줌\
        // app이라는 id를 가진 html 요소와 연결하겠다.
        el : '#app',
        //data : 인스턴스 모든 속성 저장 가능
        data : {
            message:"안녕하세요 Vue!"
        }
    })


    </script>
    
</body>
```

* example2 

> class도 연결 가능. 그러나 id와 연결이 보통. id는 유일하기 때문.

```html
<body>
    <div id="app">
        <h1>App1</h1>
        {{message}}
    </div>

    <div class="app2">
        <h1>App2</h1>
        {{message}}
    </div>


    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
    var app = new Vue({
        // Vue에서 정의한 속성 : el. el뒤에 element지정해주면 Vue의 인스턴스와 html에 그 엘리먼트를 연결해줌\
        // app이라는 id를 가진 html 요소와 연결하겠다.
        el : '#app',
        data : {
            message:"안녕하세요 Vue!"
        }
    })

    var app2 = new Vue({
        // app2이라는 class를 가진 html 요소와 연결하겠다.
        el : '.app2',
        data : {
            message:"안녕하세요 Vue!"
        }
    })


    </script>
    
</body>
```

* 같은 이름 id가 여러개일 때는 첫번째 찾은 값만 연결됨 -> app1의 결과만 뜸

```html
<body>
    <div id="app">
        <h1>App1</h1>
        {{message}}
    </div>

    <div id="app">
        <h1>App2</h1>
        {{message}}
    </div>


    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
    var app = new Vue({
        // Vue에서 정의한 속성 : el. el뒤에 element지정해주면 Vue의 인스턴스와 html에 그 엘리먼트를 연결해줌\
        // app이라는 id를 가진 html 요소와 연결하겠다.
        el : '#app',
        data : {
            message:"안녕하세요 Vue!"
        }
    })

  
    </script>
    
</body>
```

* full code

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vue Tutorial</title>
</head>
<body>
    <div id="app">
        <h1>App1</h1>
        {{message}}
        <br>
        {{number}}
    </div>

    <div id="app2">
        <span v-bind:title="message"> 내 위에 잠시 마우스를 올리면 동적으로 바인딩 된 title을 볼 수 있습니다.</span>
    </div>


    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
    var app = new Vue({
        // Vue에서 정의한 속성 : el. el뒤에 element지정해주면 Vue의 인스턴스와 html에 그 엘리먼트를 연결해줌\
        // app이라는 id를 가진 html 요소와 연결하겠다.
        el : '#app',
        data : {
            message:"안녕하세요 Vue!",
            number : 1,
        }
    })

    var app2 = new Vue({
        // Vue에서 정의한 속성 : el. el뒤에 element지정해주면 Vue의 인스턴스와 html에 그 엘리먼트를 연결해줌\
        // app2이라는 id를 가진 html 요소와 연결하겠다.
        el : '#app2',
        data : {
            // 이 메세지를 title에 쓰고 싶으면? v-bind사용
           message: '이 페이지는 ' + new Date()+ '에 로드 되었습니다.'
        }
    })


    </script>
    
</body>
</html>
```



### 반응형

> 그냥 웹에서 요소 값을 바로 바꾸면 -> 바로 반응해서 진짜 html dom에서도(웹)이 바뀜.



### 보간법

> {{ }} : 콧수염...;; 보간법 ( interpolation )
>
> ```html
> <div id="app">
>         <h1>App1</h1>
>         {{message}}
>     </div>
> ```



### Directive : v- 접두어

* v-bind: (줄여서:)

> 두개를 묶음

```html
<span v-bind:title="message"> aaa.</span>
<span :title="message"> aaa.</span>
```



```html
<body>
   
    <div id="app2">
        <span v-bind:title="message"> 내 위에 잠시 마우스를 올리면 동적으로 바인딩 된 title을 볼 수 있습니다.</span>
    </div>


    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>

    var app2 = new Vue({
        // app2이라는 id를 가진 html 요소와 연결하겠다.
        el : '#app2',
        data : {
            // 이 메세지를 title에 쓰고 싶으면? v-bind사용
           message: '이 페이지는 '+ new Date()+'에 로드 되었습니다.'
        }
    })


    </script>
    
</body>
```

*  v-if="조건"

  > 판단기준 : JS
  >
  > 조건에 들어가는 값들은 text가 아니라 속성값이다.

```html
<div id="app3">
     <!-- v-if다음 v-else넣으려면 바로 밑줄에 붙여 써야한다. -->
    <p v-if="seen">이제 나를 볼 수 있어요.</p>
    <p v-else>여긴 seen이 false일 떄 보여요.</p>

    <p v-if="num > 0">양수입니다.</p>
    <p v-else-if="num < 0">음수입니다.</p>
    <p v-else>0 입니다.</p>
</div>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.11"></script>
    <script>
        var app3 = new Vue({
            el:'#app3',
            data : {
                seen: true,
               number:1,

            }
        })
```

* v-for

> 반복시켜야하는 요소에 달기 !!!!!!!!!!(주의)
>
> ```html
>  <li v-for="(todo, idx) in todos">{{todo.text}}({{idx}})</li>
> ```
>
> 

```html
<div id="app4">
    {{todo}}
    <!-- // idx는 배열의 idx -->
    <li v-for="(todo, idx) in todos">{{todo.text}}({{idx}})</li>
</div>

<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        var app4 = new Vue({
            el : '#app4',
            data : {
                todos:[
                    {text:'JavaScript 배우기'},
                    {text:'Vue 배우기'},
                    {text:'무언가 멋진 것을 배우기'},
                    
                ]
            }
        })
   <script>
```

* v-on: (줄여서 @)

> `.enter` 하면 enter눌렀을 때만 이랑 같다.

```html
 <button v-on:click="reverseMessage">메세지 뒤집기</button>
 <button @click="reverseMessage">메세지 뒤집기</button>
```



```html
<div id='app5'>
    <p>{{message}}</p>
    <button v-on:click="reverseMessage">메세지 뒤집기</button>
    <!--<button @click="reverseMessage">메세지 뒤집기</button>-->
</div>

...

const app5 = new Vue({
            el:'#app5',
            data:{
                message:'안녕하세요! Vue.js!',
            },
            methods:{
                reverseMessage: function(event){
                    //this는 Vue안의 object=해당 인스턴스를 가리킴.
                    // this사용할거면 화살표 함수 사용하지 않고(this가 window를 가리키기 떄문) 익명함수 사용 추천. 
                    // this 사용 안하면 화살표 함수 사용 가능
                    console.log(event)
                    this.message = this.message.split('').reverse().join('')
                }
            }

        })
```

* v-model 

  > 사용자 입력 <=> data를 완전히 동기화 시키고 싶다.
  >
  > input,select,textarea(사용자 입력을 받을 수 있는 태그)에 양방향 바인딩
  >
  > input,textarea같은 입력받는 폼과 vue data와 연결시켜주는 역할
  >
  > ```html
  > <input v-model="message" type="text">
  > ```

  * 단방향 바인딩( INPUT=>DATA)

  > input이 data한테는 영향을 주지만 반대로는 아님. Vue console에서는 변경해도 변화 없음

  ```HTML
  <input #kdyup = "onInputChange" type='text'>
  ```

  * 양방향 바인딩( INPUT<=>DATA) 

  > input이 data한테는 영향을 주지만 (내가 html열었을 때 볼 수 있는 화면), 개발자툴에서 내가 수정한 값으로 변경도 됨.

  ```html
  # v-vind:value="message"와 같다.
  <input #kdyup = "onInputChange" type='text' :value="message">
  ```

  * 양방향 바인딩/v-model ( 윗줄과 완벽히 똑같은 동작함)

  ```html
  <input v-model="message" type="text">
  ```

  

```html
<div id='app6'>
    <p>input,textarea같은 입력받는 폼과 vue data와 연결시켜주는 역할</p>
    <p>{{message}}</p>
    <!-- input,textarea같은 입력받는 폼과 vue data와 연결시켜주는 역할 -->
    <input type='text' v-model='message'>
    
const app6 = new Vue({
            el:'#app6',
            data:{
                message:'안녕'
            },
        })
```

* v-show vs v-if

> v-show : dom에는 남아있고 disply:none으로 모습만 감춘다. ex() t,f가 많이 바뀔 때는 유리. 매번 다시 dom에 저장해주 않아도 되므로
>
> v-if : 조건에 맞지 않으면 아예 dom에도 없다. ex) T.F가 거의 안바뀔 때 유리. 바뀌지도 않을 v-show 개수가 많아지면 코드 낭비이므로 v-if사용하면 그냥 dom에도 안올라가므로 좋다.
>
> 장단점이 존재.

![](C:\Users\tgb03\Desktop\Vue.js\0525\v-show.PNG)

* lcuky.html 로또 번호 - `lodash` 사용 ,sort하고...

![](C:\Users\tgb03\Desktop\Vue.js\0525\lucky.PNG)

* 전체코드

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vue Directive Tutorial</title>
</head>
<body>
<div id="app3">
     <!-- v-if다음 v-else넣으려면 바로 밑줄에 붙여 써야한다. -->
    <p v-if="seen">이제 나를 볼 수 있어요.</p>
    <p v-else>여긴 seen이 false일 떄 보여요.</p>

    <p v-if="num > 0">양수입니다.</p>
    <p v-else-if="num < 0">음수입니다.</p>
    <p v-else>0 입니다.</p>
</div>

<div id="app4">
    <p>todo</p>
    <!-- // idx는 배열의 idx -->
    <li v-for="(todo, idx) in todos">{{todo.text}}({{idx}})</li>
</div>
<div id='app5'>
    <p>{{message}}</p>
    <button v-on:click="reverseMessage">메세지 뒤집기</button>
</div>

<div id='app6'>
    <p>input,textarea같은 입력받는 폼과 vue data와 연결시켜주는 역할</p>
    <p>{{message}}</p>
    <!-- input,textarea같은 입력받는 폼과 vue data와 연결시켜주는 역할 -->
    <input type='text' v-model='message'>
    
</div>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        var app3 = new Vue({
            el:'#app3',
            data : {
                seen: true,
                num: 0,

            }
        })

        var app4 = new Vue({
            el : '#app4',
            data : {
                todos:[
                    {text:'JavaScript 배우기'},
                    {text:'Vue 배우기'},
                    {text:'무언가 멋진 것을 배우기'},
                    
                ]
            }
        })
        //재할당 등으로 다른 값이 들어오지 않게 하지 위해 const 사용
        const app5 = new Vue({
            el:'#app5',
            data:{
                message:'안녕하세요! Vue.js!',
            },
            methods:{
                reverseMessage: function(event){
                    //this는 Vue안의 object=해당 인스턴스를 가리킴.
                    // this사용할거면 화살표 함수 사용하지 않고(this가 window를 가리키기 떄문) 익명함수 사용 추천. 
                    // this 사용 안하면 화살표 함수 사용 가능
                    console.log(event)
                    this.message = this.message.split('').reverse().join('')
                }
            }

        })

        const app6 = new Vue({
            el:'#app6',
            data:{
                message:'안녕'
            },
        })
    </script>
    
</body>
</html>
```



### 변수 표현법

```html
'이 페이지는 '+ new Date()+'에 로드 되었습니다.' 
`이 페이지는 ${now Date()}에 로드 되었습니다.` -> ``사용
```

