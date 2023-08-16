<script setup>
import BlockSnake from './components/BlockSnake.vue'
import { onMounted, onUnmounted, ref, computed } from 'vue'

const listBlockSnake = ref([
  {
    positionX: 200,
    positionY: 0,
    head: true
  }
])

const directionMove = ref('right')
const interval = ref(null)

const sizeScreen = computed(() => ({
  x: window.innerWidth,
  y: window.innerHeight
}))

onMounted(() => {
  window.addEventListener('keydown', logKey)
  startInterval()
})

onUnmounted(() => {
  clearInterval(interval.value)
})

const logKey = (e) => {
  clearInterval(interval.value)
  const left = 'ArrowLeft'
  const up = 'ArrowUp'
  const right = 'ArrowRight'
  const down = 'ArrowDown'

  if (e.code == up && directionMove.value !== 'up' && directionMove.value !== 'down') {
    directionMove.value = 'up'
  }
  if (e.code == down && directionMove.value !== 'up' && directionMove.value !== 'down') {
    directionMove.value = 'down'
  }
  if (e.code == left && directionMove.value !== 'left' && directionMove.value !== 'right') {
    directionMove.value = 'left'
  }
  if (e.code == right && directionMove.value !== 'left' && directionMove.value !== 'right') {
    directionMove.value = 'right'
  }
  startInterval()
}

const startInterval = () => {
  interval.value = setInterval(moveInterval, 10)
}
const moveInterval = () => {
  const positionX = listBlockSnake.value[0].positionX
  const positionY = listBlockSnake.value[0].positionY

  if (directionMove.value === 'right') {
    if (positionX >= sizeScreen.value.x) {
      listBlockSnake.value[0].positionX = 0
    } else {
      listBlockSnake.value[0].positionX += 2
    }
  }
  if (directionMove.value === 'left') {
    if (positionX <= 0) {
      listBlockSnake.value[0].positionX = sizeScreen.value.x
    } else {
      listBlockSnake.value[0].positionX -= 2
    }
  }
  if (directionMove.value === 'up') {
    if (positionY <= 0) {
      listBlockSnake.value[0].positionY = sizeScreen.value.y
    } else {
      listBlockSnake.value[0].positionY -= 2
    }
  }
  if (directionMove.value === 'down') {
    if (positionY >= sizeScreen.value.y) {
      listBlockSnake.value[0].positionY = 0
    } else {
      listBlockSnake.value[0].positionY += 2
    }
  }
}
</script>

<template>
  <header>
    <h1>Juego Snake</h1>
  </header>

  <main>
    <BlockSnake
      :position-x="listBlockSnake[0].positionX"
      :position-y="listBlockSnake[0].positionY"
    />
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}
@media (min-width: 1024px) {
  header {
    display: flex;
    flex-direction: column;
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
