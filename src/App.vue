<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addTodo="addTodo"></TodoInput>
    <TodoList v-bind:propsdata="todoItems" v-on:removeTodo="removeTodo"></TodoList>
    <TodoFooter v-on:clearAll="clearAll"></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from "./components/TodoHeader.vue";
import TodoInput from "./components/TodoInput.vue";
import TodoList from "./components/TodoList.vue";
import TodoFooter from "./components/TodoFooter.vue";

export default {
  data() {
    return {
      todoItems: []
    }
  },
  created() {
        if (localStorage.length > 0) {
            for (var i = 0; i < localStorage.length; i++) {
                var val = localStorage.key(i);
                if (val !== "loglevel:webpack-dev-server") {
                    this.todoItems.push(val);
                }
            }            
        }
    },
  methods: {
    addTodo(item) {      
      localStorage.setItem(item, item);
      this.todoItems.push(item);
    },
    clearAll() {
      localStorage.clear();
      this.todoItems = [];
    },
    removeTodo(item, index) {
      localStorage.removeItem(item);
      this.todoItems.splice(index, 1);
    }
  },
  components: {
    TodoHeader: TodoHeader,
    TodoInput: TodoInput,
    TodoList: TodoList,
    TodoFooter: TodoFooter
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
