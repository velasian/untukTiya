<script setup>
import { ref } from 'vue';

const emit = defineEmits(['prev', 'restart', 'triggerHearts']);

const isHugged = ref(false);
const openFaq = ref(null);

const faqs = [
  {
    q: '❓ "Sayang, apa sekarang kamu masih mikir aku cuma main-main?"',
    a: 'ENGGAK SAMA SEKALI SAYANG. Pemikiran itu udah lenyap 100% pas kamu jelasin tadi. Sekarang aku yakin kamu serius, dan aku makin sayang sama kamu.'
  },
  {
    q: '❓ "Gimana kalau ke depannya aku ada hal yang belum siap aku ceritain?"',
    a: 'Gak apa-apa banget cintaa. Cukup bilang: <em>"Sayang, aku belum siap cerita sekarang ya, nanti kalau udah tenang aku ceritain."</em> Aku janji gak akan maksa dan bakal nunggu sampai kamu siap.'
  }
];

function handleHug() {
  isHugged.value = true;
  emit('triggerHearts');
}

function toggleFaq(idx) {
  openFaq.value = openFaq.value === idx ? null : idx;
}
</script>

<template>
  <div class="step-card glass-card">
    <div class="tag-badge">
      <span>💌 Babak 5: Pelukan & Baikan</span>
    </div>

    <div class="heart-header pulse-heart">💌</div>

    <h2 class="step-title">Misi Terakhir: Kita Baikan ya Sayang</h2>

    <p class="step-desc">
      Tadi itu cuma salah paham karena aku panik dan kamu takut. Sekarang kita berdua udah saling ngerti isi hati masing-masing kan? Jangan ada rasa sedih lagi ya cintaku ❤️
    </p>

    <!-- Tombol Peluk Interaktif -->
    <div class="hug-section">
      <button
        type="button"
        class="hug-btn"
        @click="handleHug"
      >
        <span v-if="!isHugged">🤗 Peluk Aku (Klik Ini Biar Plong)</span>
        <span v-else>🤍 Pelukan Sudah Diterima & Sayang Kamu!</span>
      </button>

      <!-- Voucher Lucu Muncul -->
      <div v-if="isHugged" class="voucher-card animate-enter">
        <div class="voucher-stamp">RESMI</div>
        <h4>🎫 VOUCHER BAIKAN & PELUKAN</h4>
        <p>Voucher ini berlaku selamanya tanpa batas waktu! Bisa ditukar dengan pelukan paling erat dan dimanja kapan aja kita ketemu nanti 🥰</p>
        <div class="voucher-footer">
          <span>Ditandatangani dengan cinta:</span>
          <strong>Pacarmu yang paling sayang kamu 💕</strong>
        </div>
      </div>
    </div>

    <!-- Mini Tanya Jawab Tambahan -->
    <div class="faq-section">
      <span class="faq-title">Pertanyaan Kecil Buat Nemenin Kamu:</span>
      <div
        v-for="(item, idx) in faqs"
        :key="idx"
        class="faq-item"
        @click="toggleFaq(idx)"
      >
        <div class="faq-header">
          <span class="faq-q">{{ item.q }}</span>
          <span class="faq-icon">{{ openFaq === idx ? '−' : '+' }}</span>
        </div>
        <div v-if="openFaq === idx" class="faq-body animate-enter">
          <p v-html="item.a"></p>
        </div>
      </div>
    </div>

    <!-- Tombol Navigasi Akhir -->
    <div class="nav-buttons">
      <button type="button" class="btn btn-secondary nav-btn" @click="emit('prev')">
        ← Kembali
      </button>
      <button type="button" class="btn btn-outline nav-btn" @click="emit('restart')">
        Baca Lagi Dari Awal 🔄
      </button>
    </div>
  </div>
</template>

<style scoped>
.step-card {
  padding: 24px 18px;
  position: relative;
  text-align: center;
}

.tag-badge {
  display: inline-block;
  background: var(--tiya-color);
  color: #fff;
  font-size: 0.775rem;
  font-weight: 700;
  padding: 4px 12px;
  border-radius: var(--radius-full);
  margin-bottom: 12px;
}

.heart-header {
  font-size: 2.2rem;
  margin-bottom: 6px;
}

.step-title {
  font-size: 1.4rem;
  font-weight: 800;
  color: #9f1239;
  margin-bottom: 8px;
}

.step-desc {
  font-size: 0.925rem;
  color: #881337;
  line-height: 1.6;
  margin-bottom: 20px;
}

.hug-section {
  margin-bottom: 24px;
}

.hug-btn {
  width: 100%;
  max-width: 320px;
  background: linear-gradient(135deg, #e11d48 0%, #ec4899 100%);
  color: #fff;
  border: none;
  padding: 14px 20px;
  border-radius: var(--radius-full);
  font-weight: 800;
  font-size: 0.95rem;
  cursor: pointer;
  box-shadow: 0 4px 15px rgba(225, 29, 72, 0.35);
  transition: var(--transition);
}

.hug-btn:active {
  transform: scale(0.97);
}

.voucher-card {
  margin-top: 18px;
  background: #fff;
  border: 2px dashed #fda4af;
  border-radius: var(--radius-md);
  padding: 16px;
  position: relative;
  text-align: left;
  box-shadow: var(--shadow-sm);
}

.voucher-stamp {
  position: absolute;
  top: 10px;
  right: 12px;
  background: #ecfdf5;
  color: #059669;
  border: 1px solid #10b981;
  font-size: 0.7rem;
  font-weight: 800;
  padding: 2px 8px;
  border-radius: var(--radius-sm);
  transform: rotate(6deg);
}

.voucher-card h4 {
  font-size: 1rem;
  color: #be123c;
  margin-bottom: 6px;
}

.voucher-card p {
  font-size: 0.875rem;
  color: #475569;
  line-height: 1.5;
  margin-bottom: 10px;
}

.voucher-footer {
  border-top: 1px dashed #fbcfe8;
  padding-top: 8px;
  display: flex;
  flex-direction: column;
  font-size: 0.8rem;
  color: #881337;
}

.faq-section {
  text-align: left;
  margin-bottom: 20px;
}

.faq-title {
  display: block;
  font-size: 0.85rem;
  font-weight: 700;
  color: #64748b;
  margin-bottom: 8px;
}

.faq-item {
  background: rgba(255, 255, 255, 0.9);
  border: 1px solid var(--border-card);
  border-radius: var(--radius-sm);
  padding: 10px 12px;
  margin-bottom: 8px;
  cursor: pointer;
}

.faq-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 8px;
}

.faq-q {
  font-size: 0.85rem;
  font-weight: 700;
  color: var(--text-main);
}

.faq-icon {
  font-size: 1.1rem;
  color: var(--primary);
  font-weight: 700;
}

.faq-body {
  margin-top: 8px;
  padding-top: 8px;
  border-top: 1px dashed #ffe4e6;
  font-size: 0.85rem;
  color: var(--text-muted);
  line-height: 1.5;
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

.btn-outline {
  background: transparent;
  color: var(--primary);
  border: 1px solid var(--primary);
}
</style>
