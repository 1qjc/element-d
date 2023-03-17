<template>
  <el-upload
    action="#"
    list-type="picture-card"
    v-model:file-list="fileList"
    :auto-upload="false"
    :class="fileList.length && 'nihao'"
  >
    <el-icon v-if="disabled"><Plus /></el-icon>
    <template #file="{ file }">
      <div>
        <img class="el-upload-list__item-thumbnail" :src="file.url" alt="" />
        <span class="el-upload-list__item-actions">
          <span class="el-upload-list__item-preview" @click="handlePictureCardPreview(file)">
            <el-icon><zoom-in /></el-icon>
          </span>
          <span class="el-upload-list__item-delete" @click="handleDownload(file)">
            <el-icon><Download /></el-icon>
          </span>
          <span class="el-upload-list__item-delete" @click="handleRemove(file)">
            <el-icon><Delete /></el-icon>
          </span>
        </span>
      </div>
    </template>
  </el-upload>

  <el-dialog v-model="dialogVisible">
    <img w-full :src="dialogImageUrl" alt="Preview Image" />
  </el-dialog>
</template>
<script lang="ts" setup>
import { ref } from 'vue'
import { Delete, Download, Plus, ZoomIn } from '@element-plus/icons-vue'

import type { UploadFile } from 'element-plus'
const fileList = ref([])
const dialogImageUrl = ref('')
const dialogVisible = ref(false)
const disabled = ref(true)

const handleRemove = (file: UploadFile) => {
  console.log(file)
  fileList.value = []
}

const handlePictureCardPreview = (file: UploadFile) => {
  dialogImageUrl.value = file.url!
  dialogVisible.value = true
}

const handleDownload = (file: UploadFile) => {
  console.log(file)
}
</script>
<style>
.nihao .el-upload-list--picture-card .el-upload--picture-card {
  display: none;
}
</style>
