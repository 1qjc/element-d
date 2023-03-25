<template>
  <el-table
    :data="tableData"
    style="width: 100%"
    height="500px"
    :cell-style="setStyle"
    :header-cell-style="setHeaderStyle"
  >
    <el-table-column prop="date" fixed label="Date" width="180" />
    <el-table-column prop="name" label="Name" width="130" />
    <el-table-column prop="address" label="Address" min-width="180" />
    <el-table-column prop="date" label="Date" width="150" />
    <el-table-column prop="name" label="Name" width="130" />
    <el-table-column prop="address" label="Address" min-width="180" />
    <el-table-column prop="date" label="Date" width="150" />
    <el-table-column prop="name" label="Name" width="130" />
    <el-table-column prop="address" label="Address" min-width="210" />
  </el-table>
</template>

<script lang="ts" setup>
import type { CellStyle } from 'element-plus'
const tableData = [
  {
    date: '2022-04-23 12:21:66',
    name: 'Tom',
    address: 'No. 189, Grove St, Los Angeles'
  },
  {
    date: '2022-04-23 12:21:66',
    name: 'Tom',
    address: 'No. 189, Grove St, Los Angeles'
  },
  {
    date: '2022-04-23 12:21:66',
    name: 'Tom',
    address: 'No. 189, Grove St, Los Angeles'
  },
  {
    date: '2022-04-23 12:21:66',
    name: 'Tom',
    address: 'No. 189, Grove St, Los Angeles'
  },
  {
    date: '2022-04-23 12:21:66',
    name: 'Tom',
    address: 'No. 189, Grove St, Los Angeles'
  },
  {
    date: '2022-04-23 12:21:66',
    name: 'Tom',
    address: 'No. 189, Grove St, Los Angeles'
  },
  {
    date: '2022-04-23 12:21:66',
    name: 'Tom',
    address: 'No. 189, Grove St, Los Angeles'
  },
  {
    date: '2022-04-23 12:21:66',
    name: 'Tom',
    address: 'No. 189, Grove St, Los Angeles'
  },
  {
    date: '2022-04-23 12:21:66',
    name: 'Tom',
    address: 'No. 189, Grove St, Los Angeles'
  },
  {
    date: '2022-04-23 12:21:66',
    name: 'Tom',
    address: 'No. 189, Grove St, Los Angeles'
  }
]
function setStyle({ row, column, rowIndex, columnIndex }): CellStyle<any> | undefined {
  console.log({ row, column })
  const style: CellStyle<any> = {
    padding: '12px 18px',
    height: '60px',
    lineHeight: '18px',
    color: '#2c2c2c'
  }
  if (columnIndex === 0) {
    return {
      ...style,
      padding: '12px 18px 12px 48px'
    }
  }
  if (columnIndex === 8) {
    return {
      ...style,
      padding: '12px 48px 12px 18px'
    }
  }
  return style
}
function setHeaderStyle({ row, column, rowIndex, columnIndex }): CellStyle<any> | undefined {
  const style: CellStyle<any> = {
    padding: '12px 18px',
    height: '42px',
    lineHeight: '18px',
    backgroundColor: '#F7F7F7',
    color: '#000000',
    textAlign: 'center'
  }
  if (columnIndex === 0) {
    return {
      ...style,
      padding: '12px 18px 12px 48px'
    }
  }
  return style
}
</script>
<style scoped>
.el-table :deep(.cell) {
  line-height: 18px;
}
</style>
