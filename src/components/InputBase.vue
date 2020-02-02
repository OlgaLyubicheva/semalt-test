<template>
  <div :class="[haveClass ? type : 'text', {'focused' : isFocused}]" >	
    <input v-bind="$attrs" :type="type">
    <label v-if="type == 'radio'" :for="$attrs.id"><slot></slot></label>
</div>
</template>

<script>
export default {
  name: 'InputBase',
  inheritAttrs: false,
  props: {
    type: {
      type: String,
      default: 'text',
    }
  },
  computed: {
    isFocused: function () {
      return ['text', 'date'].some(item => item == this.type);
    },
    haveClass: function () {
      return ['text', 'radio', 'checkbox'].some(item => item == this.type);
    }
  }
}
</script>

<style lang="scss" scoped>
$color: var(--primary);
$radioSize: 18px;
$box-max-width: 162px;

  input {
    font: inherit;
    color: #34495D;
  }

  input:focus {
    outline: none;
  }

  .focused:focus-within {
    border-color: $color;
  }

  .part {
    position: absolute;
    top: 0;
    display: block;
    box-sizing: border-box;
    width: inherit;
    height: inherit;
    border-radius: 50%;
  }

  .radio {
    input {
      position: relative;
      width: $radioSize;
      height: $radioSize;
      vertical-align: middle;
      margin: 0 19px 3px 0;
    }

    input::before {
      @extend .part;
      content: "";
      background-color: white;
      border: 0.1rem solid $color;
      z-index: 1;
    }

    input::after {
      @extend .part;
      content: "";
      background-color: $color;
      border: 0.3rem solid transparent;
      background-clip: padding-box;
      z-index: 2;
      transform: scale(0);
      transition: transform 0.3s ease-out;
    }

    input:checked::after  {
      transform: scale(1);
    }
  }

  .text {
    position: relative;
    display: flex;
    flex-wrap: nowrap;
    box-sizing: border-box;
    width: 100%;
    min-width: fit-content;

    border: 1px solid #C2CFE0;
    background: #fff;
    border-radius: 5px;

    input {
      height: 30px;
      width: 100%;
      padding: 0 40px 0 10px;
      border: none;
      background: transparent;
    }
  }

  .checkbox {
    input {
      position: relative;
      width: $radioSize;
      height: $radioSize;
    }

    input::before {
      @extend .part;
      content: url(../assets/check-off.svg);
      z-index: 1;
    }

    input::after {
      @extend .part;
      content: url(../assets/check-on.svg);
      background-color: #fff;
      z-index: 2;
      display:none;
    }

    input:checked::after  {
      display: block;
    }
  }
</style>