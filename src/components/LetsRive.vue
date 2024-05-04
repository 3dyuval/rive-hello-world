<script setup lang="ts">
import animation from "../assets/let's_rive.riv"

import { computed, onMounted, ref } from "vue"
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

const inputs = computed(() => rive.value?.stateMachineInputs('State Machine 1'))
const trigger = (name) => inputs.value?.find(i => i.name === name)?.fire();

/*
https://rive.app/community/doc/state-machines/docxeznG7iiK

If your Rive file has Rive Listeners ( #Listeners) and you've configured your Rive instance with a state machine according to the steps outlined per runtime above, there is no additional configuration or options needed to enable the pointer events to be captured on the Rive instance. The event capturing is handled internally by the Rive widget/component.
However, if you are going about constructing your own render loop and using low-level APIs to drive Rive content, (i.e.  #Low-level API Usage) , you may need to set up event listeners manually to capture user interaction and pass feedback down to the state machine (i.e. see setup in JS).

 */
</script>

<template>
  <div>
    {{inputs}}
    <button @click="trigger('click')">Let's Rive</button>
    <canvas
            ref="canvas"
            width="400"
            height="400"
    />
  </div>
</template>
