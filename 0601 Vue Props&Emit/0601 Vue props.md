# 0601 Vue props&emit(커스텀이벤트) 

### props 사용 (부모->자식) / emit 커스텀이벤트(자식->부모)

1. (자식파일에) prop이름 ="내용"

2. (자식파일)methods설정. __커스텀이벤트__

    `$emit` : 방출 -> 이후오는 첫번째 인자는 __커스텀이벤트이름__ : 이걸로 나중에  부모파일에서 이벤트호출

   ```javascript
    methods :  {
           addTodo () {
               console.log('버튼을 눌렀습니다.')
               this.$emit('add-todo',this.newTodo)
               this.newTodo = ''
           }
       }
   ```

   

3. (부모파일) `<TodoInput @add-todo="addTodoList"/>`

* Parent.vue

```vue
<template>
  <div class="todoview">
   
    <TodoInput @add-todo="addTodoList"/>
    <TodoList :toDos="todos" @update-completed="updateCompleted"/>
     </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import TodoInput from '@/components/TodoInput.vue'
import TodoList from '@/components/TodoList.vue'
export default {
  name: 'ToDoView',
  data () {
        return{
            
            todos : [
                {content : "Django 복습하기", completed : false, id:'1'},
                {content : "Vue.js 복습하기", completed : false, id:'2'},
                {content : "JavaScript 복습하기", completed : false, id:'3'},
            ]
        }
  },
  components: {
    TodoInput,
    TodoList,
  },
  methods: {
    addTodoList(todo) {
      console.log(todo)
      if (todo.trim()){
            this.todos.push(
        {
          content : todo,
          completed : false,
          id : Date.now(),
        }
      )  
    }
  },
  updateCompleted(todo) { 
      todo.completed = !todo.completed
           
        },
  }
}
</script>

```

* TodoList.vue

```vue
<template>
  <div class="todolist">
      <h1>TodoList</h1>
      <div> 
          <!-- v-model쓰지 않은 이유 : 나중에 컴포넌트 늘어나면 디버깅에 애먹기 때문에 -->
          <!-- 데이터의 흐름이 단방향. v-model은 그냥 양방향으로 바인딩 헷갈리지 않기-->
            <!-- checkbox특성 :checked="toDo.completed" -->
         <li v-for="toDo in toDos" :key="toDo.id" :class="{completed:toDo.completed}"><input type="checkbox" :checked="toDo.completed" @click="updateCompleted(toDo)">
         {{toDo.content}}
         </li>
  
      </div>
     
  </div>
</template>

<script>
export default {
    name : 'TodoList',
    props : {
        //['toDos']이렇게 아무값이나 받아오게 할 수도 있지만
        //Validation을 위해서 아래 형식으로 받아옴.
        //String으로 받아오면 console창에서 에러가뜸
       toDos:Array,
  },
    methods: {
        
        updateCompleted (toDo) {
            this.$emit('update-completed',toDo)
        }
    }
}
</script>

<style scoped>
.completed{
    text-decoration: line-through;
    color : gray;
}
.todolist{
    padding : 0 100px;
    text-align : left;
    list-style-type:none;
}
/* scoped하면 TodoList의 h1만 css적용됨 */
h1 {
    border : solid red 2px;
}
</style>
```

* TodoInput.vue

```vue
<template>
  <div>
      <input type="text" v-model="newTodo" @keypress.enter="addTodo">
      <button @click="addTodo">할 일 목록</button>
  </div>
</template>

<script>
export default {
    name : "TodoInput",
    data () {
        return{
            newTodo : '',
        }
    },
    methods :  {
        addTodo () {
            console.log('버튼을 눌렀습니다.')
            this.$emit('add-todo',this.newTodo)
            this.newTodo = ''
        }
    }

}
</script>

<style>

</style>
```

