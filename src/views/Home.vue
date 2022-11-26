<script setup lang="ts">
import { onMounted, ref } from 'vue'
import cv from '@techstark/opencv-js'
import FilePicker from '@src/components/FilePicker.vue'

const imageUrl = ref('')
const canvas_output = ref<HTMLCanvasElement>()
const input_image = ref<HTMLImageElement>()

onMounted(() => {
})

function handleFileChange(files: File[]) {
  imageUrl.value = URL.createObjectURL(files[0])
}

function handleImageOnload() {
  if (input_image.value) {
    const mat = cv.imread(input_image.value)
    cv.imshow('canvas_output', mat)
    mat.delete()
  }
}
</script>

<template>
  <div flex flex-col p-4>
    <file-picker @file-change="handleFileChange">
      choose image
    </file-picker>
    <div flex gap-2>
      <div flex flex-col gap-2>
        <img ref="input_image" :src="imageUrl" alt="input" w-20rem @load="handleImageOnload">
        <p>input img</p>
      </div>
      <div flex flex-col gap-2>
        <canvas id="canvas_output" ref="canvas_output" w-20rem />
        <p>canvas output</p>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>
