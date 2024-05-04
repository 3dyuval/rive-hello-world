<script setup lang="ts">
import animation from "../assets/let's_rive.riv"

import { onMounted, ref } from "vue"
import { Layout, Rive } from '@rive-app/canvas'


const canvas = ref()
const rive = ref()

onMounted(() => {
  rive.value = new Rive({
    canvas: canvas!.value,
    src: animation,
    layout: new Layout({
      fit: undefined,
      alignment: undefined
    }),
    autoplay: true,
    stateMachines: ["State Machine 1"]
  })
})

const inputs = rive.value?.stateMachineInputs('State Machine 1');
// Find the input you want to set a value for, or trigger
const bumpTrigger = inputs?.find(i => i.name === 'Click');


</script>

<template>
  <div>
    <pre>{{ inputs }}</pre>
    <canvas @click="bumpTrigger.fire"
            ref="canvas"
            width="400"

            height="400"
    />
  </div>
</template>
