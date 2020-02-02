<template>
  <div class="wrapper">
    <div class="select" @click="handleDrop">
      <InputBase v-bind="$attrs" readonly :value="currentActiv"/>
    </div>
    <div :class="['options', {'options--active' : isDrop}]">
      <DropDownMenu :items="items">
        <template v-slot:menuItem="{ item }">
          <label :class="{'activ-item': item == currentActiv}">
            <input type="radio" name="options" :value="item" :checked="item == currentActiv" @change="handleSelect"/>
            {{item}}
          </label>
        </template>
      </DropDownMenu>
    </div>
    
  </div>
</template>

<script>
import InputBase from './InputBase';
import DropDownMenu from './DropDownMenu';

export default {
  name: 'Select',
  components: {
    InputBase,
    DropDownMenu,
  },
  inheritAttrs: false,
  props: {
    value: {
      type: String,
      default: '',
    },
    items: {
      type: Array,
      default: function (items) {
        return items || [];
      },
    }
  },
  data: function () {
    return {isDrop: false, currentActiv: this.value};
  },
  methods: {
    handleSelect: function (e) {
      this.currentActiv = e.target.value;
    },
    handleDrop: function () {
      const oldDrop = this.isDrop;
      this.isDrop = !oldDrop;
    }
  }
}
</script>

<style lang="scss" scoped>
  .wrapper {
    .select {
      position: relative;
    }
    .select::after {
      content: "";
      position:absolute;
      right: 0;
      top: 0;
      display: block;
      width: 30px;
      height: 100%;
      border-left: 1px solid #C2CFE0;
      background: url('../assets/select-button.svg') no-repeat;
      background-position: center center;
    }

    .options {
      display: none;

      input {
        display: none;
      }

      label {
        display: flex;
        align-items: center;
        width: 100%;
        height: 34px;
        padding: 0 18px;
      }
    }

    .options--active {
      display: block;
    }

    .activ-item {
      background-color: #F5F8FD;
    }
  }
</style>