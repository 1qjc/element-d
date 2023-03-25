<template>
  <el-descriptions :column="2" title="User Info">
    <el-descriptions-item label="Username">kooriookami</el-descriptions-item>
    <el-descriptions-item label="Telephone">18100000000</el-descriptions-item>
    <el-descriptions-item label="Place">Suzhou</el-descriptions-item>
    <el-descriptions-item label="Remarks">
      <el-tag size="small">School</el-tag>
    </el-descriptions-item>
    <el-descriptions-item label="Address">
      <div class="d">
        No.1188, Wuzhong Avenue, Wuzhong District, Suzhou, Jiangsu PrNo.1188, Wuzhong Avenue,
        Wuzhong District, Suzhou, Jiangsu ProNo.1188, Wuzhong Avenue, Wuzhong District, Suzhou,
        Jiangsu ProNo.1188, Wuzhong Avenue, Wuzhong District, Suzhou, Jiangsu ProNo.1188, Wuzhong
        Avenue, Wuzhong District, Suzhou, Jiangsu ProNo.1188, Wuzhong Avenue, Wuzhong District,
        Suzhou, Jiangsu Proovince
      </div>
    </el-descriptions-item>
  </el-descriptions>
  <el-upload
    action="https://run.mocky.io/v3/9d059bf9-4660-45f2-925d-ce80ad6c4d15"
    v-model:file-list="fileList"
    @on-change="handleChange"
    list-type="picture-card"
    :show-file-list="false"
    :auto-upload="false"
    :limit="1"
  >
    <el-icon v-if="!fileList.length"><Plus /></el-icon>
    <div v-if="fileList.length">
      <img class="el-upload-list__item-thumbnail" :src="fileList[0].url" alt="" />
      <span class="el-upload-list__item-actions">
        <span class="el-upload-list__item-preview" @click="handlePictureCardPreview(fileList[0])">
          <el-icon><zoom-in /></el-icon>
        </span>
        <span
          v-if="!disabled"
          class="el-upload-list__item-delete"
          @click="handleDownload(fileList[0])"
        >
          <el-icon><Download /></el-icon>
        </span>
        <span
          v-if="!disabled"
          class="el-upload-list__item-delete"
          @click="
            useRouter().push({
              name: 'home',
              state: { a: 2 }
            })
          "
        >
          <el-icon><Delete /></el-icon>
        </span>
      </span>
    </div>
  </el-upload>
  <button
    @click="
      useRouter().push({
        name: 'home',
        state: { a: 2 }
      })
    "
  >
    1
  </button>
  <el-dialog v-model="dialogVisible">
    <img w-full :src="dialogImageUrl" alt="Preview Image" />
  </el-dialog>
</template>

<script lang="ts" setup>
import { reactive, ref, onMounted, handleError } from 'vue'
import { useRouter } from 'vue-router'
const fileList = ref([])
onMounted(() => {})
const dialogImageUrl = ref('')
const dialogVisible = ref(false)
const disabled = ref(false)
const handleChange = () => {
  console.log(fileList.value)
}

const handlePictureCardPreview = (file: any) => {
  console.log(file)

  dialogImageUrl.value = file.url!
  dialogVisible.value = true
}
</script>

<style>
.d {
  top: -23px;
  margin-left: 60px;
  display: -webkit-box;
  -webkit-line-clamp: 1;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
</style>
