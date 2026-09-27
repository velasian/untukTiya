<script setup>
import { ref } from 'vue';

const emit = defineEmits(['next', 'triggerHearts']);
const isCooled = ref(false);

function handleCoolDown() {
  isCooled.value = true;
  emit('triggerHearts');
}
</script>

<template>
  <div class="step-card glass-card">
    <div class="author-tag">
      <span>💌 Dari: Aku</span>
      <span class="bullet">•</span>
      <span>Untuk: Kamu Sayang</span>
    </div>

    <h2 class="step-title">Sayang, Ini yang Terjadi di Hatiku Tadi Sore</h2>

    <p class="step-desc">
      Tadi sore kita sempat tegang dan salah paham ya cinta... Aku bikinin cerita bertahap ini khusus buat kamu, pakai bahasa yang paling santai dan jujur. Biar gak ada lagi rasa sedih atau tanda tanya di hatimu ya.
    </p>

    <!-- Meter Perasaan Saat Ini -->
    <div class="meter-box">
      <div class="meter-item">
        <span class="meter-icon">❌</span>
        <div>
          <span class="meter-sub">Keraguan di Hatiku</span>
          <strong class="meter-val">0% (Sudah Hilang Total)</strong>
        </div>
      </div>
      <div class="meter-sep"></div>
      <div class="meter-item">
        <span class="meter-icon">💖</span>
        <div>
          <span class="meter-sub">Perasaanku ke Kamu</span>
          <strong class="meter-val pink">100% Sayang & Bangga</strong>
        </div>
      </div>
    </div>

    <!-- Interaksi Dinginin Suasana -->
    <div class="interactive-box">
      <button
        v-if="!isCooled"
        type="button"
        class="cool-btn"
        @click="handleCoolDown"
      >
        <span>🧊 Klik Ini Dulu Biar Suasana Adem</span>
      </button>

      <div v-else class="cool-result animate-enter">
        <p>✨ <strong>Aaaah adem...</strong> Nafas dulu sebentar ya sayang. Sekarang dengerin cerita aku pelan-pelan di bawah ini yaa ❤️</p>
      </div>
    </div>

    <!-- Tombol Lanjut -->
    <div class="action-footer">
      <button type="button" class="btn btn-primary next-btn" @click="emit('next')">
        Mulai Dengerin Ceritanya 👉
      </button>
    </div>
  </div>
</template>

<style scoped>
.step-card {
  padding: 24px 18px;
  position: relative;
  overflow: hidden;
  text-align: center;
}

.author-tag {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 5px 14px;
  background: #eff6ff;
  border: 1px solid #bfdbfe;
  border-radius: var(--radius-full);
  font-size: 0.8rem;
  font-weight: 700;
  color: #2563eb;
  margin-bottom: 12px;
}

.bullet {
  color: #93c5fd;
}

.step-title {
  font-size: 1.5rem;
  font-weight: 800;
  margin-bottom: 10px;
  background: linear-gradient(135deg, #1e293b 30%, #e11d48 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.step-desc {
  font-size: 0.95rem;
  color: var(--text-muted);
  line-height: 1.6;
  margin-bottom: 20px;
}

.meter-box {
  background: rgba(255, 255, 255, 0.95);
  border: 1px solid rgba(225, 29, 72, 0.15);
  border-radius: var(--radius-md);
  padding: 14px 16px;
  display: flex;
  align-items: center;
  justify-content: space-around;
  gap: 12px;
  box-shadow: var(--shadow-sm);
  margin-bottom: 20px;
}

.meter-item {
  display: flex;
  align-items: center;
  gap: 10px;
  text-align: left;
}

.meter-icon {
  font-size: 1.3rem;
}

.meter-sub {
  display: block;
  font-size: 0.725rem;
  color: var(--text-muted);
  text-transform: uppercase;
  font-weight: 700;
}

.meter-val {
  font-size: 0.925rem;
  font-weight: 700;
  color: var(--text-main);
}

.meter-val.pink {
  color: var(--primary);
}

.meter-sep {
  width: 1px;
  height: 36px;
  background: #e2e8f0;
}

.interactive-box {
  margin: 16px 0 24px;
}

.cool-btn {
  background: #f0fdf4;
  border: 1px solid #86efac;
  color: #15803d;
  font-weight: 700;
  font-size: 0.925rem;
  padding: 12px 18px;
  border-radius: var(--radius-full);
  cursor: pointer;
  width: 100%;
  max-width: 320px;
  transition: var(--transition);
}

.cool-btn:active {
  transform: scale(0.97);
}

.cool-result {
  background: #fdf2f8;
  border: 1px solid #fbcfe8;
  padding: 12px 16px;
  border-radius: var(--radius-md);
  font-size: 0.9rem;
  color: #be185d;
}

.action-footer {
  margin-top: 10px;
}

.next-btn {
  width: 100%;
}

@media (max-width: 420px) {
  .meter-box {
    flex-direction: column;
    align-items: stretch;
  }
  .meter-sep {
    display: none;
  }
}
</style>
