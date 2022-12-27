<template>
  <t-space direction="vertical">
    <!-- 当数据为空需要占位时，会显示 cellEmptyContent -->
    <t-table
      rowKey="index"
      :data="data"
      :columns="columns"
      :stripe="stripe"
      :bordered="bordered"
      :hover="hover"
      :size="size"
      :table-layout="tableLayout ? 'auto' : 'fixed'"
      :pagination="pagination"
      :showHeader="showHeader"
      @page-change="onPageChange"
      @page-size-change="curChange"
      cellEmptyContent="-"
    ></t-table>
  </t-space>
</template>
<script lang="jsx">
const data = [];
const total = 15;
for (let i = 0; i < total; i++) {
  data.push({
    index: i,
    platform: i % 2 === 0 ? '共有' : '私有',
    type: ['String', 'Number', 'Array', 'Object'][i % 4],
  });
}
export default {
  data() {
    return {
      data,
      size: 'medium',
      tableLayout: false,
      stripe: true,
      bordered: true,
      hover: false,
      showHeader: true,

      columns: [
        {
          // 序号列，设置 colKey = serial-number 即可
          colKey: 'serial-number',
          title: '序号',
          width: 100,
        },
        {
          width: 100,
          colKey: 'platform',
          title: '平台',
        },
        {
          colKey: 'type',
          title: '类型',
          width: 100,
        },
      ],
      /** 非受控用法：与分页组件对齐 */
      pagination: {
        current: 2,
        pageSize: 5,
        total,
        currentChange: function () {
          console.log('345');
        },
      },
    };
  },
  methods: {
    onPageChange(pageInfo, newDataSource) {
      this.pagination.current = pageInfo.current;
      this.pagination.pageSize = pageInfo.pageSize;
      console.log('123', pageInfo, newDataSource);
    },
    curChange() {
      console.log('444');
    },
  },
};
</script>
