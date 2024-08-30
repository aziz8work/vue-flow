<script setup>
import { VueFlow, useVueFlow } from '@vue-flow/core'

const props = defineProps({
  position: {
    type: Object,
    required: true,
  }
})

const elements = ref([
  {
    id: '1',
    label: 'Node 1',
    position: { x: 0, y: 0 },
  },
  {
    id: '2',
    label: 'Node 2',
    position: { x: 100, y: 50 },
  },
  {
    id: 'e1-2',
    source: '1',
    target: '2'
  }
])

const isOpen = ref(false)

const { viewport } = useVueFlow()
</script> 

<template>
  <div style="background: white; border: 1px solid black; padding: 0.5rem;">
    <button @click="isOpen = !isOpen">Click to open Subflow</button>

    <Teleport to="#subflows" :disabled="!isOpen">
      <div 
        v-if="isOpen" 
        style="height: 300px; width: 300px; background: white; border: 1px dashed black;"
      >
        <VueFlow id="nested-flow" v-model="elements" fit-view-on-init />
      </div>
    </Teleport>
  </div>
</template>