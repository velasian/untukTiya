<script setup>
import { ref } from 'vue';

const emit = defineEmits(['next', 'prev', 'triggerHearts']);

const openedCards = ref({
  0: true,
  1: false,
  2: false
});

const quizAnswer = ref(null);

const promises = [
  {
    icon: '💖',
    title: '1. Aku Memilih Kamu, Bukan Keluargamu',
    desc: 'Kita gak bisa milih terlahir di keluarga kayak gimana sayang. Yang aku cintai itu diri kamu, sifat kamu, dan kebaikan hatimu. Masalah di keluargamu gak akan pernah bikin aku ilfeel atau ninggalin kamu.'
  },
  {
    icon: '🛡️',
    title: '2. Kamu Sama Sekali Gak Menyedihkan',
    desc: 'Berjuang dan rela kerja keras demi keluarga itu bukan hal yang memalukan cinta. Justru itu bukti kalau kamu wanita yang kuat dan berbakti. Aku malah makin kagum dan bangga punya kamu.'
  },
  {
    icon: '🤝',
    title: '3. Aku Mau Jadi Tempat Kamu Cerita & Pulang',
    desc: 'Kelak kalau kamu punya beban berat, bagi ke aku ya sayang. Jangan ditanggung sendirian. Aku di sini bukan buat ngehakimi kamu, tapi buat nemenin, jagain, dan sayangin kamu.'
  }
];

function toggleCard(idx) {
  openedCards.value[idx] = !openedCards.value[idx];
}

function handleQuiz(ans) {
  quizAnswer.value = ans;
  if (ans === 'right') {
    emit('triggerHearts');
  }
}
</script>

<template>
  <div class="step-card glass-card">
    <div class="tag-badge">
      <span>💖 Babak 4: Janji Hatiku yang Paling Dalam</span>
    </div>

    <h2 class="step-title">3 Hal yang Perlu Kamu Tahu dari Aku</h2>

    <p class="step-desc">
      Klik kartu di bawah ini ya sayang, biar hatimu tenang dan plong:
    </p>

    <!-- Kartu Janji yang Bisa Di-tap -->
    <div class="promise-list">
      <div
        v-for="(item, idx) in promises"
        :key="idx"
        class="promise-card"
        :class="{ expanded: openedCards[idx] }"
        @click="toggleCard(idx)"
      >
        <div class="promise-header">
          <span class="promise-icon">{{ item.icon }}</span>
          <h4 class="promise-title">{{ item.title }}</h4>
          <span class="toggle-icon">{{ openedCards[idx] ? '−' : '+' }}</span>
        </div>

        <div v-if="openedCards[idx]" class="promise-body animate-enter">
          <p>{{ item.desc }}</p>
        </div>
      </div>
    </div>

    <!-- Mini Kuis Interaktif Lucu -->
    <div class="quiz-box">
      <span class="quiz-title">🎯 Kuis Cepat: Sekarang perasaanku ke kamu gimana?</span>
      <div class="quiz-buttons">
        <button
          type="button"
          class="quiz-btn"
          :class="{ active: quizAnswer === 'wrong' }"
          @click="handleQuiz('wrong')"
        >
          🤨 Masih ragu dikit ya?
        </button>
        <button
          type="button"
          class="quiz-btn"
          :class="{ active: quizAnswer === 'right' }"
          @click="handleQuiz('right')"
        >
          🥰 100% Sayang & Bangga!
        </button>
      </div>

      <div v-if="quizAnswer === 'wrong'" class="quiz-reply wrong animate-enter">
        <p>❌ <strong>TET-TOT! Salah besar cintaku!</strong> Keraguan aku udah 0% alias hangus terbakar! Coba pilih jawaban yang satu lagi deh 😜</p>
      </div>

      <div v-if="quizAnswer === 'right'" class="quiz-reply right animate-enter">
        <p>🎉 <strong>BENERRR 100%! Pinter banget pacarku!</strong> Aku bangga banget sama kamu dan makin sayang sama kamu cintaa ❤️</p>
      </div>
    </div>

    <!-- Tombol Navigasi -->
    <div class="nav-buttons">
      <button type="button" class="btn btn-secondary nav-btn" @click="emit('prev')">
        ← Kembali
      </button>
      <button type="button" class="btn btn-primary nav-btn" @click="emit('next')">
        Misi Terakhir 👉
      </button>
    </div>
  </div>
</template>

<style scoped>
.step-card {
  padding: 24px 18px;
  position: relative;
  text-align: left;
}

.tag-badge {
  display: inline-block;
  background: var(--success);
  color: #fff;
  font-size: 0.775rem;
  font-weight: 700;
  padding: 4px 12px;
  border-radius: var(--radius-full);
  margin-bottom: 10px;
}

.step-title {
  font-size: 1.35rem;
  font-weight: 800;
  margin-bottom: 8px;
  color: var(--text-main);
}

.step-desc {
  font-size: 0.925rem;
  color: var(--text-muted);
  line-height: 1.55;
  margin-bottom: 14px;
}

.promise-list {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-bottom: 18px;
}

.promise-card {
  background: #ffffff;
  border: 1px solid var(--border-card);
  border-radius: var(--radius-md);
  padding: 12px 14px;
  cursor: pointer;
  box-shadow: var(--shadow-sm);
  transition: var(--transition);
}

.promise-card.expanded {
  border-color: #fda4af;
  background: #fffafa;
}

.promise-header {
  display: flex;
  align-items: center;
  gap: 10px;
}

.promise-icon {
  font-size: 1.3rem;
}

.promise-title {
  flex: 1;
  font-size: 0.925rem;
  font-weight: 700;
  color: var(--text-main);
}

.toggle-icon {
  font-size: 1.2rem;
  color: var(--primary);
  font-weight: 700;
}

.promise-body {
  margin-top: 10px;
  padding-top: 8px;
  border-top: 1px dashed #ffe4e6;
  font-size: 0.885rem;
  color: var(--text-muted);
  line-height: 1.6;
}

.quiz-box {
  background: rgba(255, 255, 255, 0.95);
  border: 1px solid #fed7aa;
  border-radius: var(--radius-md);
  padding: 14px;
  margin-bottom: 18px;
}

.quiz-title {
  display: block;
  font-size: 0.85rem;
  font-weight: 700;
  color: #9a3412;
  margin-bottom: 10px;
}

.quiz-buttons {
  display: flex;
  gap: 8px;
  flex-wrap: wrap;
}

.quiz-btn {
  flex: 1;
  min-width: 140px;
  background: #fff;
  border: 1px solid #cbd5e1;
  color: #334155;
  font-weight: 600;
  font-size: 0.825rem;
  padding: 10px 12px;
  border-radius: var(--radius-sm);
  cursor: pointer;
}

.quiz-btn.active {
  border-color: var(--primary);
  background: #fff1f2;
  color: var(--primary);
}

.quiz-reply {
  margin-top: 10px;
  padding: 10px 12px;
  border-radius: var(--radius-sm);
  font-size: 0.875rem;
  line-height: 1.5;
}

.quiz-reply.wrong {
  background: #fef2f2;
  border: 1px solid #fecaca;
  color: #991b1b;
}

.quiz-reply.right {
  background: #f0fdf4;
  border: 1px solid #bbf7d0;
  color: #166534;
}

.nav-buttons {
  display: flex;
  gap: 10px;
  margin-top: 16px;
}

.nav-btn {
  flex: 1;
}

.btn-secondary {
  background: #fff;
  color: var(--text-main);
  border: 1px solid #cbd5e1;
}
</style>
