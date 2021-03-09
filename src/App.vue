<template>
  <div id="app">
      <TodoHeader></TodoHeader>
      <TodoInput v-on:addTodo="addTodo"></TodoInput>
      <ListTodo v-bind:propsdata="todoItems" v-on:removeTodo="removeTodoA"></ListTodo>
      <TodoFooter v-on:removeAll="clearAll"></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput  from './components/TodoInput.vue'
import ListTodo   from './components/ListTodo.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
  data(){
    return{
      todoItems:[]
    }
  },
  created(){
    if (localStorage.length > 0 ) {
        for(var i = 0; i < localStorage.length; i++){
            if (localStorage.key(i) != "loglevel:webpack-dev-server") {
            this.todoItems.push(localStorage.key(i));
            }
        }
    }
  },
  methods:{
    addTodo(todoItem){
      localStorage.setItem(todoItem, todoItem);
      this.todoItems.push(todoItem);
    },
    clearAll(){
      localStorage.clear();
      this.todoItems = [];
    },
    removeTodoA(todoItem, index){
      localStorage.removeItem(todoItem);
      this.todoItems.splice(index, 1);
    }
  },
  components: {
    'TodoHeader'  : TodoHeader,
    'TodoInput'   : TodoInput,
    'ListTodo'    : ListTodo,
    'TodoFooter'  : TodoFooter 
  },
}
</script>

<style>
    body {
        text-align: center;
        background-color: #F6F6F8;
    }
    input {
        border-style: groove;
        width: 200px;
    }
    button {
        border-style: groove;
    }
    .shadow {
        box-shadow: 5px 10px 10px rgba(0,0,0, 0.03)
    }
</style>