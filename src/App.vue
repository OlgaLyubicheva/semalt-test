<template>
  <div id="app">
    <div class="submitted__conteiner box">
      <div class="submitted__header">
        <div>
          <h1>Submitted sitemaps <i class="info-icon"></i></h1>
        </div>
        <div class="submitted__header-actions">
          <!-- <span>Selected sitemaps: 1</span> -->
          <Button>Recrawl sitemap</Button>
          <Button secondary>Remove sitemap</Button>
        </div> 
      </div>
      <div class="submitted__filters">
        <span class="submitted__filters-title">Filters:</span>
        <div class="submitted__filters-inputs">
          <InputTextWithMenu placeholder="URL or its part"></InputTextWithMenu>
          <Select value="All types" :items="['All types']"/>
          <Select value="Submitted" :items="['Submitted']"/>
          <InputBase type="date" :value="new Date()"></InputBase>
          <Select value="All sitemaps" :items="['All sitemaps','Sitemap contains','Sitemap doesn\'t contain','Exact match']"/>
        </div>
      </div>
      <div class="submitted__table">
        <Table :tableData="sitemapsData" />
      </div>
    </div>
  </div>
</template>

<script>
import InputBase from './components/InputBase';
import Table from './components/Table';
import Button from './components/Button';
import InputTextWithMenu from './components/InputTextWithMenu';
import Select from './components/Select';

export default {
  name: 'app',
  components: {
    InputBase,
    Table,
    Button,
    InputTextWithMenu,
    Select,
  },
  data: function () {
    return {sitemapsData: []};
  },
  mounted: function () {
    const vm = this;
    fetch('./api.json')
      .then(response => response.json())
      .then(source => vm.sitemapsData = source);
  }
}
</script>

<style lang="scss">
  .submitted {
    &__conteiner {
      // @extend .box;
    }

    &__header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      height: 65px;
      padding: 0 21px;
    }

    &__filters {
      min-height: 75px;
      padding: 11px 21px;
      background: #EAEDF5;
      border: 1px solid #C2CFE0;
      box-sizing: border-box;
      overflow-x: auto;
      overflow-y: hidden;

      &-title {
        font-weight: 500;
      }

      &-inputs {
        display: flex;
        justify-content: space-between;
      }
      &-inputs>* {
        margin-right: 10px;
        width: 100%;
      }
    }
  }

  .info-icon {
    display: inline-block;
    width: 16px;
    height: 16px;
    background: url(./assets/info.svg) no-repeat; 
  }
</style>
