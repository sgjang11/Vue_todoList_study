<template>
  <div id="app">
    <todoHeader />
    <todoInput @addTodo="addTodo" />
    <todoList :propsdata="todoItems" @removeTodo="removeTodo"/>
    <todoFooter @removeAll="removeAll"/>
  </div>
</template>

<script>
import todoHeader from "./components/todoHeader.vue";
import todoInput from "./components/todoInput.vue";
import todoList from "./components/todoList.vue";
import todoFooter from "./components/todoFooter.vue";

export default {
  name: "App",
  data() {
    return {
      todoItems: []
    };
  },
  components: {
    todoHeader,
    todoInput,
    todoList,
    todoFooter
  },
  methods: {
    addTodo(todoItem){
      window.localStorage.setItem(todoItem, todoItem)
      this.todoItems.push(todoItem)
    },
    removeTodo(todoItem, index){
      localStorage.removeItem(todoItem)
      this.todoItems.splice(index,1)
    },
    removeAll(){
      localStorage.clear();
      this.todoItems=[]
    }
  },
  created() {
        if(localStorage.length > 0){
            for (let i = 0; i < localStorage.length; i++) {
                this.todoItems.push(localStorage.key(i))   
            } 
        }
    }
};
</script>

<style>
  body {
    text-align: center;
    background-color: #f6f6f8;
  }
  input {
    border-style: groove;
    width: 200px;
  }
  button {
    border-style: groove;
  }
  .shadow {
    box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
  }
</style>
