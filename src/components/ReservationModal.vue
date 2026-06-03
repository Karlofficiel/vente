<script setup lang="ts">
import { ref } from 'vue'

defineProps<{ isOpen: boolean }>()
const emit = defineEmits<{
  close: []
  submit: [data: ReservationData]
  openPayment: [data: ReservationData]
}>()

interface ReservationData {
  fullName: string
  email: string
  date: string
  vehicle: string
  message?: string
}

const form = ref<ReservationData>({
  fullName: '',
  email: '',
  date: '',
  vehicle: 'berline',
  message: '',
})

const isSubmitting = ref(false)

const vehicles = [
  { value: 'berline', label: 'Berline de Luxe' },
  { value: 'suv', label: 'SUV Premium' },
  { value: 'vip', label: 'Service VIP' },
]

const handleSubmit = async () => {
  if (!form.value.fullName || !form.value.email || !form.value.date) {
    alert('Veuillez remplir tous les champs obligatoires')
    return
  }

  isSubmitting.value = true
  emit('openPayment', form.value)
  setTimeout(() => {
    isSubmitting.value = false
  }, 300)
}

const handleClose = () => {
  if (!isSubmitting.value) {
    emit('close')
  }
}
</script>

<template>
  <div v-if="isOpen" class="modal-overlay" @click="handleClose">
    <div class="modal" @click.stop>
      <button class="modal__close" @click="handleClose" aria-label="Fermer">
        <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/>
        </svg>
      </button>

      <div class="modal__header">
        <p class="modal__label">Réserver votre trajet</p>
        <h2 class="modal__title">Une réponse sous 30 minutes</h2>
        <p class="modal__subtitle">par notre conciergerie.</p>
      </div>

      <form @submit.prevent="handleSubmit" class="modal__form">
        <div class="form-row">
          <div class="form-group">
            <label for="fullName" class="form-label">Nom Complet</label>
            <input
              id="fullName"
              v-model="form.fullName"
              type="text"
              class="form-input"
              placeholder="Jean Dupont"
              required
            />
          </div>

          <div class="form-group">
            <label for="email" class="form-label">Email</label>
            <input
              id="email"
              v-model="form.email"
              type="email"
              class="form-input"
              placeholder="contact@example.com"
              required
            />
          </div>
        </div>

        <div class="form-row">
          <div class="form-group">
            <label for="date" class="form-label">Date</label>
            <input
              id="date"
              v-model="form.date"
              type="date"
              class="form-input"
              required
            />
          </div>

          <div class="form-group">
            <label for="vehicle" class="form-label">Véhicule</label>
            <select v-model="form.vehicle" id="vehicle" class="form-input">
              <option v-for="v in vehicles" :key="v.value" :value="v.value">
                {{ v.label }}
              </option>
            </select>
          </div>
        </div>

        <div class="form-group">
          <label for="message" class="form-label">Message (Optionnel)</label>
          <textarea
            id="message"
            v-model="form.message"
            class="form-input form-textarea"
            placeholder="Détails supplémentaires..."
            rows="3"
          />
        </div>

        <button type="submit" class="btn-gold modal__submit" :disabled="isSubmitting">
          {{ isSubmitting ? 'Envoi...' : 'Confirmer la Demande' }}
        </button>
      </form>
    </div>
  </div>
</template>

<style scoped>
.modal-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.8);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
  animation: fadeIn 0.2s ease;
  backdrop-filter: blur(2px);
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

.modal {
  background: var(--color-bg-card);
  border: 1px solid var(--color-border-gold);
  width: 100%;
  max-width: 520px;
  padding: 2.5rem;
  position: relative;
  animation: slideUp 0.3s ease;
}

@keyframes slideUp {
  from {
    transform: translateY(20px);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}

.modal__close {
  position: absolute;
  top: 1.2rem;
  right: 1.2rem;
  background: none;
  border: none;
  color: var(--color-text-muted);
  cursor: pointer;
  padding: 4px;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: color 0.2s;
}

.modal__close:hover {
  color: var(--color-gold);
}

.modal__header {
  text-align: center;
  margin-bottom: 2rem;
}

.modal__label {
  font-size: 0.65rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--color-gold);
  font-weight: 600;
  margin-bottom: 0.6rem;
}

.modal__title {
  font-family: 'Playfair Display', serif;
  font-size: 1.4rem;
  color: var(--color-text);
  margin-bottom: 0.3rem;
}

.modal__subtitle {
  font-size: 0.8rem;
  color: var(--color-text-muted);
}

.modal__form {
  display: flex;
  flex-direction: column;
  gap: 1.2rem;
}

.form-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 0.4rem;
}

.form-label {
  font-size: 0.75rem;
  font-weight: 600;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: var(--color-gold);
}

.form-input {
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid var(--color-border);
  color: var(--color-text);
  padding: 0.7rem 0.9rem;
  font-size: 0.85rem;
  font-family: inherit;
  transition: border-color 0.2s, background 0.2s;
}

.form-input:focus {
  outline: none;
  border-color: var(--color-gold);
  background: rgba(255, 255, 255, 0.05);
}

.form-input::placeholder {
  color: var(--color-text-subtle);
}

.form-textarea {
  resize: vertical;
  line-height: 1.5;
}

.modal__submit {
  margin-top: 0.5rem;
  font-size: 0.8rem;
  padding: 0.85rem 1.5rem;
  letter-spacing: 0.15em;
  width: 100%;
  transition: background 0.25s, opacity 0.25s;
}

.modal__submit:disabled {
  opacity: 0.7;
  cursor: not-allowed;
}

.modal__submit:not(:disabled):hover {
  background: var(--color-gold-light);
}

@media (max-width: 600px) {
  .modal {
    width: 90%;
    max-width: none;
    padding: 2rem 1.5rem;
  }

  .form-row {
    grid-template-columns: 1fr;
  }

  .modal__title {
    font-size: 1.2rem;
  }
}
</style>
