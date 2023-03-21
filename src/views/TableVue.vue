<template>
  <el-table
    :data="tableData"
    border
    style="width: 800px"
    :cell-style="setStyle"
    :header-cell-style="{ textAlign: 'right' }"
  >
    <el-table-column prop="date" label="Date" width="180" />
    <el-table-column prop="name" label="Name" width="180" />
    <el-table-column prop="address" label="Address" />
  </el-table>
</template>

<script lang="ts" setup>
import type { CellStyle } from 'element-plus'
const tableData = [
  {
    date: new Date().toISOString(),
    name: 'Tom',
    address: 'No. 189, Grove St, Los Angeles'
  },
  {
    date: '2016-05-02',
    name: 'Tom',
    address: 'No. 189, Grove St, Los Angeles'
  },
  {
    date: '2016-05-04',
    name: 'Tom',
    address: 'No. 189, Grove St, Los Angeles'
  },
  {
    date: '2016-05-01',
    name: 'Tom',
    address: 'No. 189, Grove St, Los Angeles'
  }
]
function setStyle({ row, column, rowIndex, columnIndex }): CellStyle<any> | undefined {
  if (columnIndex == 2) {
    return {
      display: 'flex',
      justifyContent: 'center',
      textAlign: 'left'
    }
  }
}
</script>
