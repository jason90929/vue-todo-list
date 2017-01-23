<template>
  <div class="todo-wrapper">
    <hgroup>
      <h1>TODOS</h1>
      <h4>Edited by Jason Tseng</h4>
    </hgroup>
    <div class="mt-ms">
      <a href="javascript:" v-show="!isAllTodosCompleted()" class="complete-all" @click="completeAllTodos">SELECT ALL</a>
      <a href="javascript:" v-show="isAllTodosCompleted()" class="complete-all" @click="incompleteAllTodos">DESELECT ALL</a>
      <input
        type="text"
        class="todo-input todo-input-main"
        placeholder="add something..."
        v-model="newTodo"
        @keydown.enter="addTodo"
      />
    </div>
    <ul class="todo-list">
      <li v-for="(todo, index) in todos">
        <label class="label fl todo-content-item">
          <input type="checkbox" @click="completeTodo" v-model="todo.completed" />
        </label>
        <span
          v-show="!todo.editable"
          class="todo-content"
          :class="todo.completed ? 'completed' : ''"
          @dblclick="editTodo(todo);"
        >
          {{ todo.value }}
        </span>
        <input
          class="todo-input todo-content"
          v-show="todo.editable"
          v-todo-focus="todo == editedTodo"
          v-model="editedTodo"
          @blur="doneEditTodo(todo);"
          @keydown.enter="doneEditTodo(todo);"
          @keydown.esc="cancelEditTodo(todo);"
        />
        <a href="javascript:" class="flr todo-content-item" @click="removeTodo(index);">✕</a>
      </li>
    </ul>
    <div class="todo-filter">
      <span>{{ remaining }} {{ pluralize }} left</span>

      <button type="button" v-show="getCompletedTodos().length >= 1" @click="clearCompletedTodos">Clear Completed</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'todo-wrapper',
  data() {
    return {
      msg: 'Welcome to Your Vue.js App',
      newTodo: '',
      editedTodo: '',
      todos: [{
        value: 'First Todo',
        completed: true,
      }],
    };
  },
  computed: {
    remaining() {
      return this.getUncompletedTodos().length;
    },
    pluralize() {
      if (this.getUncompletedTodos().length > 1) {
        return 'items';
      }

      return 'item';
    },
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() === '') {
        return;
      }
      this.todos.push({
        value: this.newTodo.trim(),
        completed: false,
      });
      this.newTodo = '';
    },
    isAllTodosCompleted() {
      return this.todos.every(todo =>
        todo.completed === true
      );
    },
    completeAllTodos() {
      this.todos.every((todo) => {
        const Todo = todo;
        Todo.completed = true;
        return Todo;
      });
    },
    incompleteAllTodos() {
      this.todos.every((todo) => {
        const Todo = todo;
        Todo.completed = false;
        return Todo;
      });
    },
    editTodo(todo) {
      const Todo = todo;
      Todo.editable = true;
      const todoCopy = Object.assign(Todo);
      this.editedTodo = todoCopy.value;
    },
    doneEditTodo(todo) {
      if (!this.editedTodo) {
        return;
      }
      const Todo = todo;
      Todo.editable = false;
      Todo.value = this.editedTodo;
      this.editedTodo = '';
    },
    cancelEditTodo(todo) {
      const Todo = todo;
      Todo.editable = false;
      this.editedTodo = '';
    },
    completeTodo() {
      this.completed = !this.completed;
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
    getCompletedTodos() {
      return this.todos.filter((todo = {}) => todo.completed);
    },
    getUncompletedTodos() {
      return this.todos.filter((todo = {}) => !todo.completed);
    },
    clearCompletedTodos() {
      this.todos = this.getUncompletedTodos();
    },
  },
  // a custom directive to wait for the DOM to be updated
  // before focusing on the input field.
  // http://vuejs.org/guide/custom-directive.html
  directives: {
    'todo-focus': (el, value) => {
      if (value) {
        el.focus();
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
  $complete-all-w: 60px;
  .complete-all {
    font-size: 12px;
    display: inline-block;
    float: left;
    width: $complete-all-w;
    text-align: center;
    background-color: #86c380;
    height: 38px;
    line-height: 19px;
  }

  h1, h4 {
    margin: 0;
  }

  .mt-ms {
    margin-top: 20px;
  }

  .todo-input-main {
    width: calc(100% - #{$complete-all-w});
  }

  .todo-input {
    padding: 8px 10px;
    height: 38px;
    font-size: 14px;

    &:focus {
      outline: none;
    }
  }

  .todo-wrapper {
    display: block;
    background-color: #eee;
  }

  .todo-filter {
    padding: 15px 0;
  }

  ul {
    list-style-type: none;
    margin: 0 10px;
    padding: 10px 0;
  }

  li {
    display: block;
    padding: 8px 0;
    border-bottom-width: 1px;
    border-bottom-color: #64af5f;
    border-bottom-style: solid;
  }

  .completed {
    text-decoration: line-through;
  }

  a {
    color: #000;
    text-decoration: none;
  }

  .fl {
    float: left;
  }

  .flr {
    float: right;
  }

  .todo-content-item {
    width: 20px;
    height: 38px;
    line-height: 38px;
  }

  .todo-content {
    display: inline-block;
    width: calc(100% - 40px);
    height: 38px;
    line-height: 38px;
  }
</style>
