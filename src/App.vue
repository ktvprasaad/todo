<template>
  <div class="container">
    <md-field>
      <md-input v-model="currentTodo" @keydown.enter="addTodo()"
        maxlength="50" placeholder="Add a Todo"></md-input>
    </md-field>
    <ul class="todos">
      <li v-for="todo in todos" :key="todo.id">
        <input class="checked" type="checkbox" v-model="todo.completed">
        <span :class="{completed: todo.completed}" @dblclick="editTodo(todo)" v-if="!todo.edit">
          {{ todo.label }}
        </span>
        <input type="text" v-else v-model="todo.label" @keydown.enter="editDone(todo)">
        <md-button @click="removeTodo(todo)">X</md-button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      currentTodo: ''
    };
  },
  methods: {
    addTodo() {
      this.todos.push({
        id: this.todos.length, 
        label: this.currentTodo, 
        completed: false, 
        edit: false
      });
      this.currentTodo = '';
    },
    removeTodo(todo) {
      var index = this.todos.indexOf(todo);
      this.todos.splice(index,1);
    },
    editTodo(todo) {
      todo.edit = true;
    },
    editDone(todo) {
      todo.edit = false;
    }
  }
};
</script>

<style>
  .container {
    max-width: 300px;
    font-family: 'Roboto', sans-serif;
    font-size: 40px;
    display: inline;
    color: blue;
  }
  md-input {
    max-width: 200px;
    border-radius: 2px;
    border-color: blue;
  }
  li {
    list-style: none;
    margin: 10px;
  }
  .completed {
    text-decoration: line-through;
    color:coral;
  }
  md-button {
    font-size: 20px;
    /* float:right; */
  }
</style>