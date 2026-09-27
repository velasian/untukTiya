<script setup>
import { ref } from 'vue';
import ProgressBar from './ProgressBar.vue';
import StepOneIntro from '../steps/StepOneIntro.vue';
import StepTwoQuote from '../steps/StepTwoQuote.vue';
import StepThreeDomino from '../steps/StepThreeDomino.vue';
import StepFourPromises from '../steps/StepFourPromises.vue';
import StepFiveHug from '../steps/StepFiveHug.vue';
import FloatingHearts from '../effects/FloatingHearts.vue';

const currentStep = ref(1);
const totalSteps = 5;
const heartsRef = ref(null);

function scrollToTop() {
  window.scrollTo({ top: 0, behavior: 'smooth' });
}

function nextStep() {
  if (currentStep.value < totalSteps) {
    currentStep.value++;
    scrollToTop();
  }
}

function prevStep() {
  if (currentStep.value > 1) {
    currentStep.value--;
    scrollToTop();
  }
}

function goToStep(step) {
  currentStep.value = step;
  scrollToTop();
}

function restartStory() {
  currentStep.value = 1;
  scrollToTop();
  if (heartsRef.value) {
    heartsRef.value.spawnHearts(15);
  }
}

function triggerHeartsEffect(count = 14) {
  if (heartsRef.value) {
    heartsRef.value.spawnHearts(count);
  }
}
</script>

<template>
  <div class="story-wrapper">
    <!-- Floating Hearts Effect Layer -->
    <FloatingHearts ref="heartsRef" />

    <!-- Progress Indicator Bar -->
    <ProgressBar
      :currentStep="currentStep"
      :totalSteps="totalSteps"
      @goToStep="goToStep"
    />

    <!-- Active Step Renderer -->
    <main class="step-viewport">
      <transition name="step-fade" mode="out-in">
        <StepOneIntro
          v-if="currentStep === 1"
          key="step-1"
          @next="nextStep"
          @triggerHearts="triggerHeartsEffect"
        />

        <StepTwoQuote
          v-else-if="currentStep === 2"
          key="step-2"
          @next="nextStep"
          @prev="prevStep"
          @triggerHearts="triggerHeartsEffect"
        />

        <StepThreeDomino
          v-else-if="currentStep === 3"
          key="step-3"
          @next="nextStep"
          @prev="prevStep"
          @triggerHearts="triggerHeartsEffect"
        />

        <StepFourPromises
          v-else-if="currentStep === 4"
          key="step-4"
          @next="nextStep"
          @prev="prevStep"
          @triggerHearts="triggerHeartsEffect"
        />

        <StepFiveHug
          v-else-if="currentStep === 5"
          key="step-5"
          @prev="prevStep"
          @restart="restartStory"
          @triggerHearts="triggerHeartsEffect"
        />
      </transition>
    </main>
  </div>
</template>

<style scoped>
.story-wrapper {
  width: 100%;
}

.step-viewport {
  width: 100%;
}

.step-fade-enter-active,
.step-fade-leave-active {
  transition: opacity 0.3s ease, transform 0.3s ease;
}

.step-fade-enter-from {
  opacity: 0;
  transform: translateY(12px);
}

.step-fade-leave-to {
  opacity: 0;
  transform: translateY(-12px);
}
</style>
