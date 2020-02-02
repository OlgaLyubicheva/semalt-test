<template>
  <button type="button" :class="[view, {'text-secondary': secondary}]" v-bind="$attrs" >
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: 'Button',
  inheritAttrs: false,
  props: {
    view: {
      type: String,
      default: 'text'
    },
    secondary: {
      type: Boolean,
      default: false,
    }
  }
}
</script>

<style lang="scss" scoped>
  button {
    cursor: pointer;
  }
  .text {
    border: none;
    background: none;
    width: max-content;
    color: var(--primary);
    font-size: inherit;
    line-height: inherit;
    margin: 0 5px;
  }

  .text:hover {
    font-weight: 600;
  }

  .border {
    height: 25px;
    border: 1px solid var(--primary);
    border-radius: 4px;
    color: var(--primary);
    background-color: #fff;

    font-size: 13px;
    line-height: 15px;

    &:hover {
      background-color: rgba(2, 136, 209, 0.2);
    }
  }
</style>