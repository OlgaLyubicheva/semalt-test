<template>
  <div class="menu box">
    <ul>
      <li v-for="(item, i) in items" v-bind:key="i">
        <slot name="menuItem" v-bind:item="item">
        {{item}}
        </slot>
      </li>
    </ul>
    <div v-if="actions" class="menu__footer">
      <Button secondary>{{buttonsName[0]}}</Button>
      <Button>{{buttonsName[1]}}</Button>
    </div>
  </div>
  
</template>

<script>
import Button from './Button';

export default {
  name: 'DropDownMenu',
  props: {
    items: {
      type: Array,
      required: true,
    },
    actions: {
      type: Boolean,
      default: false,
    },
    buttonsName: {
      type: Array,
      default: function (data) {
        return data || ['Reset', 'Apply'];
      },
    }
  },
  components: {
    Button,
  }
}
</script>

<style lang="scss" scoped>
  .menu {
    position: absolute;
    z-index: 10;
    padding: 5px;
    width: 275px;
    box-shadow: 0px 2px 8px rgba(162, 164, 169, 0.46);

    ul {
      list-style: none;
      padding: 0;
      margin: 0;
    }

    li {
      min-height: 34px;
      display: flex;
      align-items: center;
      box-sizing: content-box;
      //padding: 12px 0;
    }

    &__footer {
      display: flex;
      justify-content: space-between;
      align-items: center;
      height: 38px;
      border-top: 1px solid #EAECEF;
    }
  }
</style>