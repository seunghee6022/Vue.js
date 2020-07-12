# Vue 복습

* vue 생성하기 `vue create <pjt name>`

```bash
vue create <pjt name>

default -> enter
(ctral+c 로 나올 수 있다)
```

* addd router하기 전에 `cd <pjt name>`
* add router ( router - url과 component를 mapping, 실제요청 일어나진 않고(완전 새로고침x), 랜더링만)

```
vue add router

history mode -> y : 나중에 페이지 정보 저장해서 뒤로가기 앞으로가기 할 수 있다.
```

* 실행하기

```
npm run serve
```

* node_modules 저장하기

> git에 올리면 node_modules가 .gitignore처리되서 다시 깔아야함.
>
> pakage.json이 있는 곳에서 `npm i`를 하면 필요한 파일들이 다 깔림

```
npm i
```



* views 폴더

  > 특정 component들은 router와 매핑되는데 이때 components폴더가 아니라 views폴더에 들어간다.

  * 구조에 너그럽다

  예를들어 App.vue에` import Helloworld from '@/components/Helloworld.vue'`처럼

  __` import Helloworld from '@/views/Home.vue'`도 가능!!!!__ 