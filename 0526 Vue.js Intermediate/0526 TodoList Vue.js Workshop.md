# 0526 TodoList Vue.js workshop

* checkbox의 상태를 v-model로 연결하기
* 인자를 ()로 넘기기 - `@click="check(todo)"` 
* 완료한 일 상태를 T/F로 나타낼 때 자료구조- todos배열에 key-value값 넣기
* 간단하게 상태 반전시키기 -` todo.completed = !todo.completed   `
* filter 사용해서 조건에 맞는 배열만 리턴하기 - `this.todos.filter(function(todo)`
* `v-bind:class` 클래스바인딩

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        .completed{
            text-decoration: line-through; 
            color:gray;
        }
    </style>
    <title>toDoList</title>
</head>
<body>
    <div id='app'>
        <h1>To Do List</h1>
        <select v-model='status'>
            <option value='all' >전체</option>
            <option value='active' >진행중</option>
            <option value='done' >완료</option>
        </select>

        <ul>
            <li v-for='todo in todoByStatus' :key="todo.id" v-if ='!todo.completed' :class="{completed:todo.completed}">    
                    <input type='checkbox' v-model="todo.completed">{{todo.title}} 
            </li>
            <li class='completed' v-else><input type='checkbox' v-model="todo.completed">{{todo.title}} 
            </li>
        </ul>
        <input type='text' v-model='newTodo'>
        <button @click='addTodoList(newTodo)'>+</button>
        <br>
        <button @click='deleteCompleted(todos)'>완료된 할 일 지우기</button>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

    <script>
      
        const app = new Vue({
            el : '#app',
            data : {
                todos:[
                {
                    id : 1,
                    title:'Django 복습',
                    completed : false,
                },
                {   
                    id : 2,
                    title:'JavaScript 복습',
                    completed : false,
                },
                {
                    id : 3,
                    title : '병원 가기',
                    completed: true,
                },
                {
                    id : 4,
                    title : '물리치료 받기',
                    completed: false,
                },
                
                ],
                newTodo : '',
                status : 'all',
            },
            methods : {
                check : function(todo){
                    todo.completed = !todo.completed   
                    if (todo.completed){console.log(todo.title,"완료")}
                    else {console.log(todo.title,"완료 취소")}
                },
                
                addTodoList : function(newTodo){
                    console.log(this.newTodo)
                    if (this.newTodo.length) {
                        this.todos.push(
                        {
                        id : Date.now(),
                        title : this.newTodo,
                        completed:false,
                        }
                    )                   
                    this.newTodo = ''
                    }
                   
                },
                deleteCompleted : function (todos) {
                    //filter: cB(callback)함수의 return에 작성된 값으로 필터링한 결과를 
                    const notCompTodos = this.todos.filter(function (todo) {
                        // return 조건 : 완료되지 않은 값들로만 배열을 만들어 리턴
                        return !todo.completed
                    })
                    console.log(notCompTodos)
                    this.todos = notCompTodos
            
                },
                
            },

        computed : {
            todoByStatus : function () {
                    if (this.status==='active'){
                        return this.todos.filter(todo =>{
                            return !todo.completed
                        })
                    }
                    else if (this.status === 'done'){
                        return this.todos.filter(todo=>{
                            return todo.completed
                        })
                    }
                    else {
                        return this.todos
                    }
                }
            },
        })
    </script>
</body>
</html>
```

### HTML 클래스 바인딩

https://kr.vuejs.org/v2/guide/class-and-style.html

적용하고 싶은 태그에다가 `class='completed'` 클래스 설정

* `:class='{completed:todo.completed}'`  or `:class='{'completed':todo.completed}'` 와 같이 사용

* 클래스명에 -사용 불가

  

```html
 <style>
        .completed{
            text-decoration: line-through; 
            color:gray;
        }
    </style>

<li v-for='todo in todoByStatus()' :key= v-if='!todo.completed' :class="{completed:todo.completed}">    
                    <input type='checkbox' v-model="todo.completed">{{todo.title}} 
            </li>
            <li class='completed' v-else><input type='checkbox' v-model="todo.completed">{{todo.title}} 
            </li>
```

### Dropdown

```html
<select v-model='status'>
            <option value='all' >전체</option>
            <option value='active' >진행중</option>
            <option value='done' >완료</option>
        </select>

  computed : {
            todoByStatus : function () {
                    if (this.status==='active'){
                        return this.todos.filter(todo =>{
                            return !todo.completed
                        })
                    }
                    else if (this.status === 'done'){
                        return this.todos.filter(todo=>{
                            return todo.completed
                        })
                    }
                    else {
                        return this.todos
                    }
                }
            },
        })
```



### for문 순서 오류 방지위해 id 설정

* id 설정가능한 unique값 : 시간 `Date.now()`

* `:key="todo.id" `

```javascript
  <li v-for='todo in todoByStatus' :key="todo.id" v-if ='!todo.completed' :class="{completed:todo.completed}">    
                    <input type='checkbox' v-model="todo.completed">{{todo.title}} 
            </li>
            <li class='completed' v-else><input type='checkbox' v-model="todo.completed">{{todo.title}} 
            </li>

addTodoList : function(newTodo){
                    console.log(this.newTodo)
                    if (this.newTodo.length) {
                        this.todos.push(
                        {
                        id : Date.now(),
                        title : this.newTodo,
                        completed:false,
                        }
                    )                   
                    this.newTodo = ''
                    }
                   
```

### computed vs methods

> 함수내용을 computed에 넣으면 변수로 사용 가능. -> 함수는 매번 실행되야 해서 서버에 부담을 주지만, computed는 오직 read만 하므로 최적화 가능.
>
> computed는 데이터 변경이 일어나지 않는 이상 캐싱된 데이터를 가지고 쓰고, methods는 매번 새로 불러온다.

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Computed vs Methods</title>
</head>
<body>
    <div id='app'>
    <button @click="visible = !visible">Switch</button>
    <ul v-if='visible'>
        <li>Computed:{{ methodsDate() }}</li>
        <li> Methods:{{ computedDate }}</li>
    </ul>
</div>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        const app = new Vue({
            el:'#app',
            data:{
                visible : true,
            },
            methods: {
                    methodsDate : function () {
                        return new Date()
                    }
            },
           
           
            computed: {
                computedDate : function () {
                    return new Date()
            }
            }
        })
   
    </script>
</body>
</html>
```

