<script setup>
import { computed } from 'vue'
const props = defineProps({
  positionX: {
    type: Number,
    default: 0
  },
  positionY: {
    type: Number,
    default: 0
  }
})
const styleBlock = computed(() => ({
  position: 'absolute',
  width: '10px',
  height: '10px',
  backgroundColor: '#ff0000',
  transform: `translate(${props.positionX}px, ${props.positionY}px)`
}))
</script>

<template>
  <div :style="styleBlock" />
</template>
