<template>
  <div>
    <el-input type="textarea" rows="4" v-model="content" resize="none" />
    <div v-if="isTyping">...</div>
    <div v-else>{{ content }}</div>
  </div>
</template>
<script setup lang="ts">
const content = ref('')
const isTyping = ref(false)
watch(content, (newId, oldId, onCleanup) => {
  if (content.value.length > 0) {
    isTyping.value = true
    const t = setTimeout(() => {
      isTyping.value = false
    }, 200)
    onCleanup(() => {
      clearTimeout(t)
    })
  }
})
</script>
