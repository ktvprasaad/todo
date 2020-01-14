<template>
  <div class="container">
    <div class="todoBox">
    <md-field>
      <md-input class="md-focussed" v-model="currentTodo" @keydown.enter="addTodo(todo)"
        placeholder="Key-in Todo Tasks"></md-input>
      <md-button class="md-primary" @click="addTodo(todo)">
        Add
      </md-button>
    </md-field>
    </div>

    <ul class="todos">
      <li v-for="todo in todos" :key="todo.id">
        <md-checkbox class="md-primary" type="checkbox" v-model="todo.completed">+</md-checkbox>
        <!-- <input> -->
        <!-- <md-checkbox v-model="todo.completed"> -->
        <!-- <input md-checked v-model="todo.completed"> -->
         <span :class="{completed: todo.completed}" @dblclick="editTodo(todo)" v-if="!todo.edit">
          {{ todo.label }}
          </span>
        <input type="text" v-else v-model="todo.label" @keydown.enter="editDone(todo)">
        <md-button @click="removeTodo(todo)">
          <img src="./assets/del.png" alt="delete task">
        </md-button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'RegularCheckboxes',
  data() {
    return {
      todos: [],
      currentTodo: ''
    };
  },
  methods: {
    addTodo() {
      if (this.currentTodo.length > 0) {
        this.todos.push({
          id: this.todos.length, 
          label: this.currentTodo, 
          completed: false, 
          edit: false
        });
      }
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
    margin: auto;
    font-family: 'Roboto', sans-serif;
    font-size: 24px;
    display: inline;
  }
  .todoBox {
    margin: 20px;
  }
  li {
    list-style: none;
    margin-bottom: 7px;
  }
  .completed {
    text-decoration: line-through;
    color:coral;
  }
  .md-checkbox {
    /* display: flex; */
    align-items: center;
  }
</style>