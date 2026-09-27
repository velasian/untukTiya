<script setup>
import { ref } from 'vue';

const emit = defineEmits(['next', 'prev', 'triggerHearts']);

const isSmashed = ref(false);

const steps = [
  {
    num: '1️⃣',
    title: 'Kamu Takut Dibilang "Menyedihkan"',
    desc: 'Kamu punya rencana kerja ke LN karena keadaan keluarga, tapi kamu takut aku mandang kamu rendah. Jadi tadi kamu jawab: <em>"Gak ada plan apa-apa sayang."</em>'
  },
  {
    num: '2️⃣',
    title: 'Kamu Keceplosan Cerita Kerja ke LN',
    desc: 'Waktu aku cerita mimpiku mau sekolah ke LN, kamu keceplosan bilang mau kerja ke LN juga. Di situ aku bingung: <em>"Lho, tadi katanya gak ada rencana, kok sekarang ada?"</em>'
  },
  {
    num: '3️⃣',
    title: 'Aku Panik & Keceplosan Pasang Tameng',
    desc: 'Karena belum tahu alasan aslimu, aku takut dipermainkan. Akhirnya tadi keluarlah kata-kata tamengku: <em>"Kamu cuma main-main ya? Kalau gitu aku imbangin aja."</em>'
  },
  {
    num: '4️⃣',
    title: 'Kamu Berani Jujur Soal Masalah Keluarga',
    desc: 'Kamu kasih tahu kalau keluargamu lagi ada masalah dan kamu terpaksa ambil jalan itu. Pintu rahasianya terbuka, dan aku akhirnya mengerti seutuhnya.'
  }
];

function smashBlocks() {
  isSmashed.value = true;
  emit('triggerHearts');
}
</script>

<template>
  <div class="step-card glass-card">
    <div class="tag-badge">
      <span>🧩 Babak 3: Alur Salah Paham Tadi</span>
    </div>

    <h2 class="step-title">Gimana Ceritanya Kok Bisa Sampai Sana?</h2>

    <p class="step-desc">
      Biar gampang dibayangin, alur salah paham tadi itu cuma kayak 4 kartu ini sayang:
    </p>

    <!-- Daftar 4 Balok Domino -->
    <div v-if="!isSmashed" class="domino-stack">
      <div
        v-for="(item, idx) in steps"
        :key="idx"
        class="domino-card"
      >
        <span class="domino-num">{{ item.num }}</span>
        <div class="domino-text">
          <h5>{{ item.title }}</h5>
          <p v-html="item.desc"></p>
        </div>
      </div>

      <!-- Tombol Hancurkan -->
      <div class="smash-action">
        <button type="button" class="smash-btn" @click="smashBlocks">
          💥 Klik Buat Hancurin Semua Salah Paham Ini!
        </button>
      </div>
    </div>

    <!-- Tampilan Setelah Dihancurkan -->
    <div v-else class="smashed-result animate-enter">
      <div class="smashed-icon">💥 ➔ 🕊️ ➔ 💖</div>
      <h3>BOOM! RUNTUH JADI ABU!</h3>
      <p class="smashed-main">
        Begitu tadi kamu jujur bilang: <em>"Keluargaku lagi gak baik-baik saja..."</em>
      </p>
      <div class="smashed-box">
        <p>
          Semua praduga <em>"kamu main-main"</em> dan rasa <em>"ragu"</em> di kepalaku 
          <strong>LANGSUNG HANCUR LEBUR JADI ABU</strong>.
        </p>
        <p>
          Aku langsung sadar kalau kamu bukan orang yang main-main, tapi kamu justru wanita hebat yang lagi mikirin keluarganya. 
          Semua keraguanku tadi <strong>HILANG 100%</strong>!
        </p>
      </div>
    </div>

    <!-- Tombol Navigasi -->
    <div class="nav-buttons">
      <button type="button" class="btn btn-secondary nav-btn" @click="emit('prev')">
        ← Kembali
      </button>
      <button type="button" class="btn btn-primary nav-btn" @click="emit('next')">
        Lanjut ke Janjiku 👉
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
  background: var(--rey-color);
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
  margin-bottom: 16px;
}

.domino-stack {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-bottom: 16px;
}

.domino-card {
  display: flex;
  align-items: flex-start;
  gap: 12px;
  background: #ffffff;
  padding: 12px 14px;
  border-radius: var(--radius-md);
  border: 1px solid rgba(0, 0, 0, 0.06);
  box-shadow: var(--shadow-sm);
}

.domino-num {
  font-size: 1.2rem;
  line-height: 1.2;
}

.domino-text h5 {
  font-size: 0.925rem;
  font-weight: 700;
  margin-bottom: 2px;
}

.domino-text p {
  font-size: 0.85rem;
  color: var(--text-muted);
  line-height: 1.5;
  margin: 0;
}

.smash-action {
  margin-top: 10px;
}

.smash-btn {
  width: 100%;
  background: linear-gradient(135deg, #f43f5e 0%, #e11d48 100%);
  color: #fff;
  font-weight: 800;
  font-size: 0.95rem;
  padding: 14px;
  border-radius: var(--radius-md);
  border: none;
  cursor: pointer;
  box-shadow: 0 4px 15px rgba(225, 29, 72, 0.35);
  transition: var(--transition);
}

.smash-btn:active {
  transform: scale(0.97);
}

.smashed-result {
  background: linear-gradient(135deg, #ecfdf5 0%, #d1fae5 100%);
  border: 2px solid #34d399;
  border-radius: var(--radius-lg);
  padding: 20px 16px;
  text-align: center;
  margin-bottom: 20px;
}

.smashed-icon {
  font-size: 2rem;
  margin-bottom: 6px;
}

.smashed-result h3 {
  font-size: 1.25rem;
  font-weight: 800;
  color: #065f46;
  margin-bottom: 8px;
}

.smashed-main {
  font-size: 0.925rem;
  color: #047857;
  margin-bottom: 12px;
}

.smashed-box {
  background: rgba(255, 255, 255, 0.8);
  border-radius: var(--radius-md);
  padding: 12px 14px;
  font-size: 0.9rem;
  color: #065f46;
  line-height: 1.6;
  display: flex;
  flex-direction: column;
  gap: 8px;
  text-align: left;
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
