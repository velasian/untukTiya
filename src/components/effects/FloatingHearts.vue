<script setup>
import { ref } from 'vue';

const hearts = ref([]);
let nextId = 0;

function spawnHearts(count = 12) {
  const emojis = ['💖', '💕', '❤️', '🌸', '✨', '🥰', '🤍'];
  for (let i = 0; i < count; i++) {
    const id = nextId++;
    const heart = {
      id,
      emoji: emojis[Math.floor(Math.random() * emojis.length)],
      left: Math.random() * 85 + 5 + '%',
      size: Math.random() * 14 + 18 + 'px',
      duration: Math.random() * 1.5 + 2 + 's',
      delay: Math.random() * 0.3 + 's'
    };
    hearts.value.push(heart);
    setTimeout(() => {
      hearts.value = hearts.value.filter(h => h.id !== id);
    }, 3500);
  }
}

defineExpose({ spawnHearts });
</script>

<template>
  <div class="hearts-container" aria-hidden="true">
    <span
      v-for="h in hearts"
      :key="h.id"
      class="floating-heart"
      :style="{
        left: h.left,
        fontSize: h.size,
        animationDuration: h.duration,
        animationDelay: h.delay
      }"
    >
      {{ h.emoji }}
    </span>
  </div>
</template>

<style scoped>
.hearts-container {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  pointer-events: none;
  overflow: hidden;
  z-index: 9999;
}

.floating-heart {
  position: absolute;
  bottom: -40px;
  animation: floatUp ease-out forwards;
  will-change: transform, opacity;
}

@keyframes floatUp {
  0% {
    transform: translateY(0) scale(0.6) rotate(0deg);
    opacity: 1;
  }
  50% {
    transform: translateY(-50vh) scale(1.2) rotate(15deg);
    opacity: 0.9;
  }
  100% {
    transform: translateY(-110vh) scale(1) rotate(-15deg);
    opacity: 0;
  }
}
</style>
