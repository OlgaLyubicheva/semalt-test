<template>
  <table class="table">
    <thead>
      <tr>
        <th></th>
        <th>Sitemap</th>
        <th>Type</th>
        <th>Submitted</th>
        <th>Last check</th>
        <th>Status</th>
        <th>URLs</th>
        <th>Recrawl sitemap</th>
        <th>Remove sitemap</th>
      </tr>
    </thead>
    <tbody>
      <TableRow v-for="(row, i) in tableData" :rowData="row" :key="i"/>
    </tbody>
  </table>
</template>

<script>
import TableRow from './TableRow';

export default {
  name: 'Table',
  props: {
    tableData: {
      type: Array,
      default: function (data) {
        return data || [];
      },
    }
  },
  data: function () {
    return { isChecked: [] };
  },
  components: {
    TableRow,
  }
}
</script>

<style lang="scss" scoped>
  .table {
    width: 100%;
    text-align: center;
    border-collapse: collapse;
    overflow: hidden;

    thead {
      tr {
        height: 50px;
      }
      background: #F6F8FE;
    }

    tbody {
      tr {
      height: 64px;
    }

    
    td {
      min-width: 30px;
      max-width: calc((100% - 30px)/8);
      padding: 10px;
    }
    }
  }
  
</style>