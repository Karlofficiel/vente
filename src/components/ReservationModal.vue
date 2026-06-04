<script setup lang="ts">
import { ref } from 'vue'

// Interface pour les données de réservation
interface ReservationData {
  fullName: string
  email: string
  date: string
  vehicle: string
  message?: string
}

defineProps<{ isOpen: boolean }>()

// Déclaration propre des événements (emits)
const emit = defineEmits<{
  (e: 'close'): void
  (e: 'open-payment', data: ReservationData): void
}>()

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
  // Correction de la condition de validation (ajout des ||)
  if (!form.value.fullName || !form.value.email || !form.value.date) {
    alert('Veuillez remplir tous les champs obligatoires')
    return
  }

  isSubmitting.value = true
  
  // On envoie les données vers le module de paiement
  emit('open-payment', form.value)
  
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
          <line x1="18" y1="6" x2="6" y2="18"/>
          <line x1="6" y1="6" x2="18" y2="18"/>
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
            placeholder="Précisez des détails ou des demandes spécifiques..."
            rows="3"
          ></textarea>
        </div>

        <button type="submit" class="btn-gold modal__submit" :disabled="isSubmitting">
          {{ isSubmitting ? 'Traitement...' : 'Continuer vers le paiement' }}
        </button>
      </form>
    </div>
  </div>
</template>

<style scoped>
.modal-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.85);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
  padding: 1.5rem;
}

.modal {
  background: #0d0d0d;
  border: 1px solid var(--color-border-gold, #c5a880);
  width: 100%;
  max-width: 650px;
  padding: 2.5rem;
  position: relative;
  border-radius: 4px;
}

.modal__close {
  position: absolute;
  top: 1rem;
  right: 1rem;
  background: none;
  border: none;
  color: #fff;
  cursor: pointer;
  opacity: 0.7;
  transition: opacity 0.2s;
}

.modal__close:hover {
  opacity: 1;
}

.modal__header {
  text-align: center;
  margin-bottom: 2rem;
}

.modal__label {
  font-size: 0.8rem;
  text-transform: uppercase;
  color: var(--color-gold, #c5a880);
  letter-spacing: 0.1em;
}

.modal__title {
  font-family: 'Playfair Display', serif;
  font-size: 1.8rem;
  color: #fff;
  margin: 0.5rem 0;
}

.modal__subtitle {
  color: #888;
  font-size: 0.9rem;
}

.modal__form {
  display: flex;
  flex-direction: column;
  gap: 1.2rem;
}

.form-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1.2rem;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 0.4rem;
}

.form-label {
  font-size: 0.8rem;
  color: #ccc;
}

.form-input {
  background: #141414;
  border: 1px solid #222;
  color: #fff;
  padding: 0.8rem;
  border-radius: 4px;
  font-size: 0.9rem;
  width: 100%;
  outline: none;
  transition: border-color 0.2s;
}

.form-input:focus {
  border-color: var(--color-gold, #c5a880);
}

.form-textarea {
  resize: none;
}

.modal__submit {
  width: 100%;
  padding: 1rem;
  background: var(--color-gold, #c5a880);
  color: #000;
  border: none;
  font-weight: bold;
  cursor: pointer;
  text-transform: uppercase;
  font-size: 0.8rem;
  letter-spacing: 0.1em;
  transition: background 0.2s;
  margin-top: 1rem;
}

.modal__submit:hover {
  background: #d4b990;
}

.modal__submit:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

@media (max-width: 600px) {
  .form-row {
    grid-template-columns: 1fr;
  }
}
</style>
