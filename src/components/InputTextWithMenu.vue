<template>
  <div class="wrapper">
    <div class="input">
      <InputBase v-bind="$attrs"/>
    </div>
    <div class="menu-input">
      <DropDownMenu  actions :items="['Sitemap contains','Sitemap doesn\'t contain','Exact match']">
        <template v-slot:menuItem="{ item }">
          <div class="menu-input__item">
            <InputBase type="radio" name="searchParam" :value="item" :checked="item == 'Sitemap contains'">{{item}}</InputBase>
          </div>
        </template>
      </DropDownMenu>
    </div>
    
  </div>
</template>

<script>
import InputBase from './InputBase';
import DropDownMenu from './DropDownMenu';

export default {
  name: 'InputTextWithMenu',
  components: {
    InputBase,
    DropDownMenu,
  },
  inheritAttrs: false,
}
</script>

<style lang="scss" scoped>
  .wrapper {
    //min-width: fit-content;

    .menu-input {
      display: none;

      &__item {
        padding: 12px 18px;
        //min-width: fit-content;
      }
    }

    .menu-input:hover {
      display: block;
    }

    .input:hover + .menu-input {
      display: block;
    }
  }
</style>