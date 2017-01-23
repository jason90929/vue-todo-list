<template>
  <div class="todo-wrapper">
    <div>
      <a href="javascript:" v-show="!isAllTodosCompleted()" class="complete-all" @click="completeAllTodos">SELECT ALL</a>
      <a href="javascript:" v-show="isAllTodosCompleted()" class="complete-all" @click="uncompleteAllTodos">DESELECT ALL</a>
      <input
        type="text"
        class="todo-input"
        placeholder="add something..."
        v-model="newTodo"
        @keydown.enter="addTodo"
      />
    </div>
    <ul class="todo-list">
      <li v-for="(todo, index) in todos">
        <label class="label fl">
          <input type="checkbox" @click="completeTodo" v-model="todo.completed" />
        </label>
        <span :class="todo.completed ? 'completed' : ''">{{ todo.value }}</span>
        <a href="javascript:;" class="flr" @click="removeTodo(index);">X</a>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'todo-wrapper',
  data() {
    return {
      msg: 'Welcome to Your Vue.js App',
      newTodo: '',
      todos: [{
        value: 'First Todo',
        completed: true,
      }],
    };
  },
  methods: {
    addTodo() {
      this.todos.push({
        value: this.newTodo,
        completed: false,
      });
      this.newTodo = '';
    },
    isAllTodosCompleted() {
      let allTodosCompleted = true;
      this.todos.map((todo) => {
        const Todo = todo;
        if (!Todo.completed) {
          allTodosCompleted = false;
        }

        return null;
      });

      return allTodosCompleted;
    },
    completeAllTodos() {
      this.todos.map((todo) => {
        const Todo = todo;
        Todo.completed = true;
        return Todo;
      });
    },
    uncompleteAllTodos() {
      this.todos.map((todo) => {
        const Todo = todo;
        Todo.completed = false;
        return Todo;
      });
    },
    completeTodo() {
      this.completed = !this.completed;
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
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

  .todo-input {
    width: calc(100% - #{$complete-all-w});
    padding: 8px 10px;
    height: 38px;
    font-size: 14px;
  }

  .todo-wrapper {
    display: block;
    background-color: #eee;
  }

  ul {
    list-style-type: none;
    margin: 0 10px;
    padding: 0;
  }

  li {
    display: block;
    padding: 8px 0;

    + li {
      border-top-width: 1px;
      border-top-color: #64af5f;
      border-top-style: solid;
    }
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
</style>
