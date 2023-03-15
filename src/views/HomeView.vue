<template>
  <div>
    <audio src=""></audio>
    <video src=""></video>
  </div>
</template>
<script setup lang="ts">
import { ref } from 'vue'
const b = { red: 'red' }
const a = ref('red')
defineExpose({ a })
</script>
<style>
.hah {
  display: flex;
}
.red {
  color: red;
}
.label {
  color: var(--el-text-color-primary);
}
.text {
  color: var(--el-text-color-regular);
  margin-left: 16px;
  width: 400px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
</style>
