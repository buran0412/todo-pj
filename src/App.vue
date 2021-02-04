<template>
  <div id="app">
    <div class="container">
      <div class="card">
        <p>Todo List</p>
        <span></span><input v-model="task" class="input-add" />
        <button class="add" v-on:click="addTodo">追加</button>
        <todo-list v-on:remove="removeTodo" v-bind:items="todos"></todo-list>
      </div>
    </div>
  </div>
</template>

<script>
import TodoList from "../src/components/TodoList.vue";

export default {
  name: "app",
  components: {
    TodoList,
  },
  data: function() {
    return {
      task: "",
      todos: [],
      count: 0,
    };
  },
  methods: {
    addTodo: function() {
      if (this.task === "") {
        alert("作業名を入力してください");
        return;
      }
      this.todos.push({
        message: this.task,
        id: ++this.count,
      });
      this.task = "";
    },
    removeTodo: function(event, index) {
      this.todos.splice(index, 1);
    },
    editTodo: function(event, index) {
      this.todos.splice(index, 1);
    },
  },
  mounted: function() {
    this.todos = JSON.parse(localStorage.getItem("todos")) || [];
    // this.todos = [];
    const todos = this.todos;
    this.count = this.todos.length;
    window.onbeforeunload = function() {
      localStorage.setItem("todos", JSON.stringify(todos));
    };
  },
};
</script>

<style>
.container {
  background-color: #2d197c;
  height: 100vh;
  width: 100vw;
  position: relative;
}

.card {
  background-color: #fff;
  width: 50vw;
  padding: 30px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  border-radius: 10px;
  font-weight: bold;
  font-size: 24px;
}

.input-add {
  width: 80%;
  padding: 5px;
  border-radius: 5px;
  border: 1px solid #ccc;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  font-size: 14px;
  outline: none;
}

.add {
  text-align: left;
  border: 2px solid #dc70fa;
  font-size: 12px;
  color: #dc70fa;
  background-color: #fff;
  font-weight: bold;
  padding: 8px 16px;
  border-radius: 5px;
  cursor: pointer;
  transition: 0.4s;
  outline: none;
}
</style>
