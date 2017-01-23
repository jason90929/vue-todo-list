<template>
  <button
    type="button"
    class="btn"
    :class="buttonClassInit"
  >
    <span>
      {{value}}
    </span>
  </button>
</template>

<script>
export default {
  name: 'button',
  props: {
    value: {
      type: String,
      default: 'Submit',
    },
    color: {
      type: String,
    },
    size: {
      type: String,
    },
  },
  computed: {
    buttonClassInit() {
      let className = '';
      if (this.color) {
        className += `btn--color-${this.color}`;
      }
      if (this.size) {
        className += ` btn--size-${this.size}`;
      }

      return className;
    },
  },
};

</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
  @import "../assets/styles/variables";

  button {
    &:focus {
      outline: none;
    }
  }

  .btn {
    border: 0;
    background-color: $white;
    font-size: 14px;
    text-transform: uppercase;

    &--color {
      &-red {
        color: $white;
        background-color: #e20821;
      }

      &-blue {
        color: $white;
        background-color: #352ce2;
      }
    }

    &--size {
      &-md {
        padding: 8px 16px;
      }

      &-sm {
        padding: 5px 12px;
      }
    }
  }
</style>
