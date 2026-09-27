<script setup>
defineProps({
  currentStep: {
    type: Number,
    required: true
  },
  totalSteps: {
    type: Number,
    default: 5
  }
});

const emit = defineEmits(['goToStep']);

const stepLabels = [
  'Awalan',
  'Pesan Tadi',
  'Kenapa Begitu',
  'Janji Aku',
  'Baikan'
];
</script>

<template>
  <div class="progress-wrapper">
    <div class="progress-info">
      <span class="step-counter">Babak {{ currentStep }} dari {{ totalSteps }}</span>
      <span class="step-label">{{ stepLabels[currentStep - 1] }}</span>
    </div>

    <div class="progress-bar-track">
      <div
        class="progress-bar-fill"
        :style="{ width: ((currentStep) / totalSteps) * 100 + '%' }"
      ></div>
    </div>

    <div class="step-dots">
      <button
        v-for="s in totalSteps"
        :key="s"
        type="button"
        class="step-dot"
        :class="{ active: s === currentStep, completed: s < currentStep }"
        :title="'Lompat ke langkah ' + s"
        @click="emit('goToStep', s)"
      >
        <span v-if="s < currentStep">✓</span>
        <span v-else>{{ s }}</span>
      </button>
    </div>
  </div>
</template>

<style scoped>
.progress-wrapper {
  margin-bottom: 20px;
  background: rgba(255, 255, 255, 0.85);
  padding: 12px 14px;
  border-radius: var(--radius-md);
  border: 1px solid var(--border-card);
  box-shadow: var(--shadow-sm);
}

.progress-info {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 0.825rem;
  font-weight: 700;
  margin-bottom: 8px;
}

.step-counter {
  color: var(--primary);
}

.step-label {
  color: var(--text-muted);
  background: #fff1f2;
  padding: 2px 10px;
  border-radius: var(--radius-full);
}

.progress-bar-track {
  width: 100%;
  height: 8px;
  background: #f1f5f9;
  border-radius: var(--radius-full);
  overflow: hidden;
  margin-bottom: 12px;
}

.progress-bar-fill {
  height: 100%;
  background: linear-gradient(90deg, #ec4899 0%, #e11d48 100%);
  border-radius: var(--radius-full);
  transition: width 0.4s cubic-bezier(0.4, 0, 0.2, 1);
}

.step-dots {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.step-dot {
  width: 28px;
  height: 28px;
  border-radius: 50%;
  border: 1px solid #cbd5e1;
  background: #fff;
  color: var(--text-muted);
  font-size: 0.75rem;
  font-weight: 700;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: var(--transition);
}

.step-dot.active {
  background: var(--primary);
  color: #fff;
  border-color: var(--primary);
  transform: scale(1.15);
  box-shadow: 0 2px 8px rgba(225, 29, 72, 0.35);
}

.step-dot.completed {
  background: #ecfdf5;
  color: #059669;
  border-color: #a7f3d0;
}
</style>
