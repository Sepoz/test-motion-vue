<script setup>
import { Motion } from 'motion-v'

const container = {
  hidden: { opacity: 1, scale: 0 },
  visible: {
    opacity: 1,
    scale: 1,
  },
}

const items = {
  hidden: { y: 20, opacity: 0, scale: 0.85 },
  visible: {
    y: 0,
    opacity: 1,
  },
}

const list = [0, 1, 2, 3]
</script>

<template>
  <main class="container">
    <Motion
      class="motion-primary"
      :initial="{ scale: 0 }"
      :animate="{ rotate: 180, scale: 1 }"
      :transition="{
        type: 'spring',
        stiffness: 260,
        damping: 20,
        delay: 0.3,
      }"
    />

    <Motion
      class="motion-primary"
      :animate="{
        scale: [1, 0.5, 0.5, 1, 1],
        rotate: [0, 0, 180, 180, 0],
        borderRadius: ['0%', '0%', '20%', '20%', '0%'],
      }"
      :transition="{
        duration: 2,
        ease: 'easeInOut',
        times: [0, 0.2, 0.5, 0.8, 1],
        repeat: Infinity,
      }"
    />

    <Motion
      as="ul"
      :variants="container"
      initial="hidden"
      animate="visible"
      :transition="{
        type: 'spring',
        delayChildren: 0.5,
        staggerChildren: 0.2,
      }"
      class="motion-container"
    >
      <Motion v-for="item in list" :key="item" :variants="items" class="motion-primary" />
    </Motion>
  </main>
</template>

<style scoped>
.container {
  width: 100vw;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  row-gap: 100px;
}

.motion-primary {
  background-color: burlywood;
  width: 33%;
  aspect-ratio: 1/1;
  border-radius: 10px;
  transform-origin: center;
}

.motion-container {
  border-radius: 1rem;
  overflow: hidden;
  list-style: none;
  padding: 0.5rem;
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-template-rows: repeat(2, 1fr);
  aspect-ratio: 1 / 1;
  background-color: rgba(222, 184, 135, 0.2);
  width: 33%;
}
</style>
