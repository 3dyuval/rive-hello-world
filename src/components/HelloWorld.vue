<script setup lang="ts">

import { onMounted, ref } from "vue"
import { Layout, Rive } from '@rive-app/canvas'


const props = defineProps<{
  src: string
  fit: string
  alignment: string
}>()

const canvas = ref()

onMounted(() => {

  const rive = new Rive({
    canvas: canvas!.value,
    src: props.src,
    layout: new Layout({
      fit: props.fit,
      alignment: props.alignment
    }),
    autoplay: true
  })
})
</script>

<template>
  <div>
    <canvas ref="canvas" width="400" height="400"></canvas>
  </div>
</template>
