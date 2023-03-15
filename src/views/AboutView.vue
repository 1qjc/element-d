<template>
  <el-form :model="form" label-width="120px">
    <el-form-item label="Activity type">
      <el-checkbox-group v-model="form.type">
        <el-checkbox label="Online activities" name="type" />
        <el-checkbox label="Promotion activities" name="type" />
        <el-checkbox label="Offline activities" name="type" />
        <el-checkbox label="Simple brand exposure" name="type" />
      </el-checkbox-group>
    </el-form-item>
    <el-form-item label="Resources">
      <el-radio-group v-model="form.resource">
        <el-radio label="Sponsor" />
        <el-radio label="Venue" />
      </el-radio-group>
    </el-form-item>
    <el-form-item label="Activity form"> </el-form-item>
    <div class="box" style="height: 200px">
      <el-input v-model="form.desc" type="textarea" />
      <el-icon><CirclePlus /></el-icon>
      <el-input v-model="form.desc" type="textarea" />
      <el-icon><CirclePlus /></el-icon> <el-input v-model="form.desc" type="textarea" />
      <el-icon><CirclePlus /></el-icon> <el-input v-model="form.desc" type="textarea" />
      <el-icon><CirclePlus /></el-icon> <el-input v-model="form.desc" type="textarea" />
      <el-icon><CirclePlus /></el-icon>
    </div>
    <el-form-item>
      <el-button type="primary" @click="onSubmit">Create</el-button>
      <el-button>Cancel</el-button>
    </el-form-item>
  </el-form>
  <home-view ref="home"></home-view>
</template>

<script lang="ts" setup>
import { reactive, ref, onMounted } from 'vue'
import HomeView from './HomeView.vue'
const home = ref(null)
onMounted(() => {
  console.log(home.value)
})
// do not use same name with ref
const form = reactive({
  name: '',
  region: '',
  date1: '',
  date2: '',
  delivery: false,
  type: [],
  resource: '',
  desc: ''
})

const onSubmit = () => {
  console.log('submit!')
}
</script>

<style>
.box {
  padding: 20px;
  overflow-y: scroll;
  border: 1px var(--el-border-color) solid;
  border-radius: var(--el-border-radius-base);
  margin: 12px 24px;
}
</style>
