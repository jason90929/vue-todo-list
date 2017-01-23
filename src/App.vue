<template>
  <div id="app">
    <div class="container">
      <TodoWrapper />
    </div>
  </div>
</template>

<script>
import TodoWrapper from './components/TodoWrapper';

export default {
  name: 'app',
  components: {
    TodoWrapper,
  },
};
</script>

<style lang="scss">
  * {
    -webkit-box-sizing: border-box;
    box-sizing: border-box;
  }

  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }

  .container {
    position: relative;
    max-width: 480px;
    margin: 0 auto;
  }
</style>
