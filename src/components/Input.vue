<template>
  <input
    type="text"
    class="input"
    :class="inputClassInit"
  />
</template>

<script>
export default {
  name: 'input',
};

</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
  @import "../assets/styles/variables";

  .input {
    font-size: 14px;
    line-height: 24px;
    margin: 0;
    padding: 3px 8px;
    border-width: 1px;
    border-style: solid;
    border-color: #999;

    &:focus {
      outline: none;
    }
  }
</style>
