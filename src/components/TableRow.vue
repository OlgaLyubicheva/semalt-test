<template>
  <tr>
    <td><InputBase type="checkbox"/></td>
    <td class="td-path"><a :href="rowData.path" target="_blank">{{'/' + rowData.path.split('/').reverse()[0]}}</a></td>
    <td>{{rowData.isSitemapsIndex ? 'Sitemaps index' : ''}}</td>
    <td>{{parseDate(rowData.lastSubmitted)}}</td>
    <td>{{parseDate(rowData.lastCheck)}}</td>
    <td :class="rowData.warnings == 0 && rowData.errors == 0 ? 'td-ok' : 'td-error'">
      {{rowData.warnings == 0 && rowData.errors == 0 ? 'Success' : `Warnings: ${rowData.warnings}, errors: ${rowData.errors}`}}
    </td>
    <td>{{rowData.urls}}</td>
    <td><Button view='border'>Recrawl</Button></td>
    <td>
      <Button>
        <svg width="14" height="20" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path class="trash-icon" d="M1 17.7778C1 19 1.9 20 3 20H11C12.1 20 13 19 13 17.7778V6.66667C13 5.44444 12.1 4.44444 11 4.44444H3C1.9 4.44444 1 5.44444 1 6.66667V17.7778ZM13 1.11111H10.5L9.79 0.322222C9.61 0.122222 9.35 0 9.09 0H4.91C4.65 0 4.39 0.122222 4.21 0.322222L3.5 1.11111H1C0.45 1.11111 0 1.61111 0 2.22222C0 2.83333 0.45 3.33333 1 3.33333H13C13.55 3.33333 14 2.83333 14 2.22222C14 1.61111 13.55 1.11111 13 1.11111Z"/>
        </svg>
      </Button>
    </td>
  </tr>
</template>

<script>
import Button from './Button';
import InputBase from './InputBase';

export default {
  name: 'TableRow',
  components: {
    Button,
    InputBase,
  },
  props: {
    rowData: {
      type: Object,
      required: true,
    }
  },
  methods: {
    parseDate: function (str) {
      const month = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'];
      const date = new Date(str);
      return `${month[date.getMonth()]} ${date.getDate()}, ${date.getFullYear()}`;
    }
  }
}
</script>

<style lang="scss" scoped>
tr {
  height: 64px;
}
   
td {
  min-width: 30px;
  max-width: calc((100% - 30px)/8);
  padding: 10px;
}

.trash-icon {
  fill: #9FA2B4;

  &:hover {
    fill: #FB6868;
  }
}

.td-path {
  a {
    color: var(--primary);
    text-decoration: none;
  }
  
  a::after {
    content:url(../assets/link.svg);
    margin-left: 7px;
  }
}

.td-ok {
  color: var(--green);
}

.td-error {
  color: var(--secondary);
}

</style>