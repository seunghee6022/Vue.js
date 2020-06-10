# 0609 Vue-for-Django - login, logout, signup

* download

```bash
#0608에서 했던것들 다운로드
#0609
python -m pip install django-cors-headers

vue create articlefront
cd articlefront
vue add router
```

---



* settings.py

```python
ALLOWED_HOSTS = ['*']


# Application definition

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'articles',
    'accounts',

    # DRF
    'rest_framework',
    'rest_framework.authtoken',
    'rest_auth',

    'django.contrib.sites',
    'allauth',
    'allauth.account',
    'rest_auth.registration',

    # CORS
    'corsheaders',
]

MIDDLEWARE = [
    # CORS
    'corsheaders.middleware.CorsMiddleware',
    # 'django.middleware.common.CommonMiddleware',

    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]



LANGUAGE_CODE = 'ko-kr'

TIME_ZONE = 'Asia/Seoul'


SITE_ID = 1

#DRF auth settings
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework.authentication.BasicAuthentication',
        'rest_framework.authentication.SessionAuthentication',
    ]
}

# auth user를 새롭게 정의했으므로 기존 유저 더이상 사용 불가
AUTH_USER_MODEL = 'accounts.User'


CORS_ORIGIN_ALLOW_ALL = True
```

* App.vue

```vue

```

* Create.vue

```vue
<template>
  <div>
      <h1>New Article</h1>
      Title : 
      <br>
      <input type='text' v-model="newArticle.title">
      <br>
      Content :
      <br>
      <textarea cols="30" rows="30" v-model="newArticle.content"></textarea>
      <br>
      <button @click='createArticle'>Submit</button>
  </div>
</template>

<script>
import axios from 'axios'
const BASE_URL = 'http://127.0.0.1:8000'
export default {
name : 'Create',
data() {
    return {
        newArticle : {
            title : '',
            content : '',    
        }
    }
},
methods : {
    createArticle() {      
        const requestHeaders = {
            headers : {
                Authorization : 'Token ' + this.$cookies.get('auth-token')
            }
        }
        axios.post(BASE_URL+'/articles/create/', this.newArticle, requestHeaders)
        .then( res => {
            console.log(res)
        })
        .catch( err => {
            console.log(err.response)
        })
       
}
}
}
</script>

<style>

</style>
```

* Home.vue

```vue
<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <br>
   <button @click='getList'>getList</button>
   <br>
   <ul>
       <li v-for="article in articles" :key='article.id'>
            {{article.title}}
       </li>
   </ul>
  
  </div>
</template>

<script>
import axios from 'axios'
const BASE_URL = 'http://127.0.0.1:8000'


export default {
  name: 'Home',
  data() {
      return {
          articles : [],
      }
  },
  methods: {
      getList() {
          axios.get(BASE_URL+'/articles/')
          .then(res => {
              console.log(res)
              this.articles = res.data
          })
          .catch(err=>{
              console.log(err.response)
          })
      }
  }

  
}
</script>

```

* Login.vue

```vue
<template>
  <div>
    <h1>Login</h1>
    username : <input type='text' v-model='loginData.username'>
    <br>
    password : <input type='password' v-model='loginData.password'>
    <br>
    <button @click="login">Login</button>
  </div>
</template>

<script>
export default {
  name: 'Login',
  data () {
    return{
      loginData :{
    username : null,
    password : null
    }
    }
  },
  methods : {
    login() {
      console.log("Login.vue",this.loginData)
      this.$emit('login', this.loginData)
    }
  }
}
</script>

```

* Signup.vue

```vue
<template>
  <div>
    <h1>Signup</h1>
    username : 
    <br>
    <input type='text' v-model='signupData.username'>
    <br>
    password : 
    <br>
    <input type='password' v-model='signupData.password1'>
    <br>
    password confirmation: 
    <br>
    <input type='password' v-model='signupData.password2'>
    <br>
    <button @click='signup'>Sumbit</button>
    
  </div>
</template>

<script>
export default {
name : 'Signup',
data () {
    return{
        signupData : {
            username : null,
            password1 : null,
            password2 : null,
        }
    }
},
methods : {
    signup(signupData){
        this.$emit('signup',this.signupData)
    }
},
}
</script>

<style>

</style>
```

