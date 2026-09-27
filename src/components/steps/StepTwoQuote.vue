<script setup>
import { ref } from 'vue';

const emit = defineEmits(['next', 'prev', 'triggerHearts']);

const isRevealed = ref(false);
const selectedReaction = ref(null);

function revealReason() {
  isRevealed.value = true;
}

function handleReaction(type) {
  selectedReaction.value = type;
  emit('triggerHearts');
}
</script>

<template>
  <div class="step-card glass-card">
    <div class="tag-badge">
      <span>💬 Babak 2: Pesan yang Bikin Kamu Kaget Tadi</span>
    </div>

    <h2 class="step-title">Kenapa Tadi Aku Sampai Ngomong Gini?</h2>

    <p class="step-desc">
      Tadi kamu sempat soroti dan nanya kenapa aku bisa ngomong dua kalimat ini kan sayang:
    </p>

    <!-- Kotak Pesan yang Disorot -->
    <div class="quote-box">
      <p class="quote-line">"Kamu cuman mau main main aja ya? Gak ada niat serius juga?"</p>
      <p class="quote-line">"Jika memang kamu ga ada niatan yaa gak masalah sih, aku imbangin aja"</p>
    </div>

    <!-- Interaksi Buka Rahasia -->
    <div class="reveal-section">
      <button
        v-if="!isRevealed"
        type="button"
        class="reveal-btn"
        @click="revealReason"
      >
        <span>🫣 Klik Buat Bongkar Isi Kepalaku Saat Itu</span>
      </button>

      <div v-else class="revealed-content animate-enter">
        <div class="letter-bubble">
          <p>
            <strong>Pertama, aku minta maaf ya sayang...</strong> Waktu tadi beneran gak ada niat jahat sedikit pun buat nyakitin kamu.
          </p>
          <p>
            Waktu tadi kamu bilang <em>"nggak ada rencana"</em> terus tiba-tiba bilang <em>"ada rencana kerja ke luar negeri"</em>, kepalaku langsung korslet dan parno sayang.
          </p>
        </div>

        <div class="shield-grid">
          <div class="shield-card rey">
            <h5>🛡️ Tameng Rasa Takutku Sendiri</h5>
            <p>
              Kata-kata <em>"aku imbangin aja"</em> itu sebenarnya <strong>tameng rasa takutku</strong>. Aku takut banget kalau ternyata cuma aku yang serius, sedangkan kamu nggak. Jadi aku pura-pura bersikap dingin biar gak kelihatan patah hati sendirian.
            </p>
          </div>

          <div class="shield-card tiya">
            <h5>💔 Yang Dirasain Hati Kamu Sayang</h5>
            <p>
              Kamu kaget dan sedih karena merasa langsung dituduh jahat, padahal kamu nutupin itu karena ada beban keluarga yang bikin kamu malu dan takut cerita.
            </p>
          </div>
        </div>

        <!-- Pilihan Reaksi Lucu/Interaktif -->
        <div class="reaction-prompt">
          <span class="prompt-text">Jujur, reaksi kamu pas baca itu tadi gimana?</span>
          <div class="reaction-buttons">
            <button
              type="button"
              class="reaction-btn"
              :class="{ active: selectedReaction === 'mad' }"
              @click="handleReaction('mad')"
            >
              😤 Kesel & Nyebelin!
            </button>
            <button
              type="button"
              class="reaction-btn"
              :class="{ active: selectedReaction === 'sad' }"
              @click="handleReaction('sad')"
            >
              🥺 Sedih, padahal nahan beban...
            </button>
          </div>

          <div v-if="selectedReaction === 'mad'" class="reaction-reply animate-enter">
            <p>🥺 <strong>Ampun sayang...</strong> Aku tahu itu nyebelin banget. Aku minta maaf yaa. Waktu tadi aku panik berlebihan, sekarang aku udah sadar dan janji gak akan nuduh sembarangan lagi ❤️</p>
          </div>

          <div v-if="selectedReaction === 'sad'" class="reaction-reply animate-enter">
            <p>🫂 <strong>Peluk erat cintaku...</strong> Aku nyesel banget udah bikin kamu makin sedih. Kamu wanita hebat udah kuat nanggung itu, ke depannya kamu gak sendirian lagi ya sayang ❤️</p>
          </div>
        </div>
      </div>
    </div>

    <!-- Tombol Navigasi -->
    <div class="nav-buttons">
      <button type="button" class="btn btn-secondary nav-btn" @click="emit('prev')">
        ← Kembali
      </button>
      <button type="button" class="btn btn-primary nav-btn" @click="emit('next')">
        Lanjut ke Alurnya 👉
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
  background: #f43f5e;
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

.quote-box {
  background: #fff1f2;
  border-left: 4px solid #f43f5e;
  border-radius: var(--radius-sm);
  padding: 12px 14px;
  margin-bottom: 16px;
}

.quote-line {
  font-size: 0.925rem;
  font-weight: 700;
  color: #9f1239;
  line-height: 1.45;
  margin-bottom: 4px;
}

.quote-line:last-child {
  margin-bottom: 0;
}

.reveal-btn {
  width: 100%;
  background: linear-gradient(135deg, #fdf2f8 0%, #eff6ff 100%);
  border: 1px solid #fbcfe8;
  color: #be123c;
  font-weight: 700;
  font-size: 0.925rem;
  padding: 14px 16px;
  border-radius: var(--radius-md);
  cursor: pointer;
  margin-bottom: 20px;
  transition: var(--transition);
}

.reveal-btn:active {
  transform: scale(0.98);
}

.letter-bubble {
  background: #f8fafc;
  border-radius: var(--radius-md);
  padding: 12px 14px;
  font-size: 0.9rem;
  line-height: 1.6;
  color: #334155;
  margin-bottom: 12px;
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.shield-grid {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-bottom: 16px;
}

.shield-card {
  padding: 12px 14px;
  border-radius: var(--radius-md);
  font-size: 0.885rem;
  line-height: 1.5;
}

.shield-card.rey {
  background: #f0f7ff;
  border: 1px solid #bfdbfe;
}

.shield-card.tiya {
  background: #fdf2f8;
  border: 1px solid #fbcfe8;
}

.shield-card h5 {
  font-size: 0.925rem;
  margin-bottom: 4px;
}

.shield-card.rey h5 {
  color: #1e40af;
}

.shield-card.tiya h5 {
  color: #be185d;
}

.reaction-prompt {
  background: rgba(255, 255, 255, 0.95);
  border: 1px solid #e2e8f0;
  border-radius: var(--radius-md);
  padding: 14px;
  margin-bottom: 20px;
}

.prompt-text {
  display: block;
  font-size: 0.85rem;
  font-weight: 700;
  color: #475569;
  margin-bottom: 10px;
}

.reaction-buttons {
  display: flex;
  gap: 8px;
  flex-wrap: wrap;
}

.reaction-btn {
  flex: 1;
  min-width: 140px;
  background: #f1f5f9;
  border: 1px solid #cbd5e1;
  color: #334155;
  font-weight: 600;
  font-size: 0.825rem;
  padding: 10px 12px;
  border-radius: var(--radius-sm);
  cursor: pointer;
  transition: var(--transition);
}

.reaction-btn.active {
  background: #ffe4e6;
  border-color: #f43f5e;
  color: #9f1239;
}

.reaction-reply {
  margin-top: 12px;
  background: #fff7ed;
  border: 1px solid #fed7aa;
  padding: 10px 12px;
  border-radius: var(--radius-sm);
  font-size: 0.875rem;
  color: #9a3412;
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
</style>
