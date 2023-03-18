<template>
  <el-upload
    action="https://run.mocky.io/v3/9d059bf9-4660-45f2-925d-ce80ad6c4d15"
    list-type="picture-card"
    v-model:file-list="fileList"
    :auto-upload="false"
    drag
    :class="fileList.length && 'nihao'"
    :on-preview="handlePictureCardPreview"
  >
    <el-icon><Plus /></el-icon>
  </el-upload>
  <el-dialog v-model="dialogVisible">
    <img w-full :src="dialogImageUrl" alt="Preview Image" />
  </el-dialog>
</template>
<script lang="ts" setup>
import { ref } from 'vue'
import { Plus } from '@element-plus/icons-vue'
import type { UploadFile } from 'element-plus'
const fileList = ref([])
const dialogImageUrl = ref('')
const dialogVisible = ref(false)

const handlePictureCardPreview = (file: UploadFile) => {
  dialogImageUrl.value = file.url!
  dialogVisible.value = true
}
</script>
<style scoped>
.w {
  width: 100px;
  height: 100px;
}
.nihao :deep(.el-upload-list--picture-card .el-upload--picture-card) {
  display: none;
}
</style>
