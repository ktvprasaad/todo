<template>
  <div class="container">
    <div class="todoBox">
    <md-field>
      <md-input class="md-focussed" v-model="currentTodo" @keydown.enter="addTodo(todo)"
      placeholder="Key-in tasks!" maxlength="50"></md-input>
      <md-button id="add" class="md-primary" @click="addTodo(todo)">
        Add
      </md-button>
    </md-field>
    </div>

    <ul class="todos">
      <li v-for="todo in todos" :key="todo.id">
        <md-checkbox type="checkbox" title="done" class="md-primary" v-model="todo.completed"></md-checkbox>
         <span :class="{completed: todo.completed}" @dblclick="editTodo(todo)" v-if="!todo.edit">
          {{ todo.label }}
          </span>
        <md-input type="text" v-else v-model="todo.label" @keydown.enter="editDone(todo)"></md-input>
        <md-button id="del" title="delete" @click="removeTodo(todo)">
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
    font-family: 'Roboto', sans-serif;
    font-size: 24px;
    display: inline;
  }
  .todoBox {
    margin: 20px;
    display: block;
  }
  li {
    list-style: none;
    margin-bottom: 7px;
  }
  .completed {
    text-decoration: line-through;
    color:#C3E86C;
  }
  /* .md-checkbox { */
    /* display: flex; */
    /* align-items: center;
  } */
  .md-input {
    border-bottom: 2px solid #5321DD !important;
    max-width: 360px;
    margin: 0 auto;
  }
  .md-checkbox {
    background-color: #C3E86C;
  }
  /* .md-button:hover { */
    /* border-radius: 90%; */
    /* background-color: #C3E86C !important;
  } */
  #add, #add:hover {
    background-color: #5321DD !important;
    color: white;
  }
  #del:hover {
    background-color: #C3E86C;
  }
  .todos {
    color: #5321DD;
  }
</style>