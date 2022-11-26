<script setup lang="ts">
import { ref } from 'vue'

interface Props {
  accept?: string
  multiple?: boolean
}

withDefaults(defineProps<Props>(), {
  accept: 'image/*',
  multiple: false,
})

const emit = defineEmits(['fileChange'])

const file_picker = ref()

function selectFile() {
  file_picker.value?.click()
}

async function handleFileChange() {
  const { files } = file_picker.value
  emit('fileChange', files)
}
</script>

<template>
  <div @click="selectFile">
    <input
      ref="file_picker"
      type="file"
      :accept="accept"
      :multiple="multiple"
      class="hidden"
      @change="handleFileChange"
    >
    <slot />
  </div>
</template>

<style>
</style>
