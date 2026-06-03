<script setup lang="ts">
import { ref } from 'vue'

defineProps<{
  isOpen: boolean
  reservationData?: {
    fullName: string
    email: string
    date: string
    vehicle: string
  } | null
}>()

const emit = defineEmits<{
  close: []
  pay: [data: PaymentData]
}>()

interface PaymentData {
  amount: number
  method: string
  phone: string
}

const form = ref<PaymentData>({
  amount: 0,
  method: 'orange-money',
  phone: '',
})

const isProcessing = ref(false)

const paymentMethods = [
  {
    id: 'orange-money',
    name: 'Orange Money',
    icon: 'orange',
    description: 'Paiement via Orange Money',
    color: '#FF6B35',
  },
  {
    id: 'mtn-money',
    name: 'MTN Money',
    icon: 'mtn',
    description: 'Paiement via MTN Money',
    color: '#FFD60A',
  },
  {
    id: 'motn-money',
    name: 'Motn Money',
    icon: 'motn',
    description: 'Paiement via Motn Money',
    color: '#06A77D',
  },
]

const amountPresets = [5000, 10000, 25000, 50000, 100000]

const handlePayment = async () => {
  if (!form.value.amount || !form.value.phone) {
    alert('Veuillez remplir tous les champs')
    return
  }

  if (form.value.phone.length < 8) {
    alert('Numéro de téléphone invalide')
    return
  }

  isProcessing.value = true

  const methodNames: Record<string, string> = {
    'orange-money': 'Orange Money',
    'mtn-money': 'MTN Money',
    'motn-money': 'Motn Money',
  }

  const whatsappNumber = '693747572'
  const message = `Demande de paiement:\n\nRéservation: ${form.value.amount} FCFA\nMéthode: ${methodNames[form.value.method]}\nTéléphone: ${form.value.phone}\nVéhicule: ${form.value.method}`

  const whatsappUrl = `https://wa.me/${whatsappNumber}?text=${encodeURIComponent(message)}`

  setTimeout(() => {
    window.open(whatsappUrl, '_blank')
    emit('close')
    form.value = { amount: 0, method: 'orange-money', phone: '' }
    isProcessing.value = false
  }, 500)
}

const handleClose = () => {
  if (!isProcessing.value) {
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
        <p class="modal__label">Paiement Sécurisé</p>
        <h2 class="modal__title">Confirmez votre Paiement</h2>
      </div>

      <form @submit.prevent="handlePayment" class="modal__form">
        <div class="form-group">
          <label class="form-label">Montant (FCFA)</label>
          <div class="amount-input-group">
            <input
              v-model.number="form.amount"
              type="number"
              class="form-input"
              placeholder="Entrez le montant"
              min="1000"
              required
            />
          </div>
          <div class="presets">
            <button
              v-for="preset in amountPresets"
              :key="preset"
              type="button"
              class="preset-btn"
              @click.prevent="form.amount = preset"
            >
              {{ preset.toLocaleString() }}
            </button>
          </div>
        </div>

        <div class="form-group">
          <label class="form-label">Numéro de Téléphone</label>
          <input
            v-model="form.phone"
            type="tel"
            class="form-input"
            placeholder="Ex: 693747572"
            required
          />
        </div>

        <div class="form-group">
          <label class="form-label">Méthode de Paiement</label>
          <div class="payment-methods">
            <label v-for="method in paymentMethods" :key="method.id" class="payment-method">
              <input
                v-model="form.method"
                type="radio"
                :value="method.id"
                class="payment-method__input"
              />
              <div class="payment-method__content" :style="{ '--color': method.color }">
                <div class="payment-method__icon">
                  <svg v-if="method.icon === 'orange'" width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
                    <circle cx="12" cy="12" r="10"/>
                    <circle cx="12" cy="12" r="6" fill="white" opacity="0.2"/>
                  </svg>
                  <svg v-else-if="method.icon === 'mtn'" width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
                    <path d="M12 2 L22 8 L22 16 L12 22 L2 16 L2 8 Z"/>
                  </svg>
                  <svg v-else width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
                    <rect x="3" y="5" width="18" height="14" rx="2"/>
                  </svg>
                </div>
                <div class="payment-method__text">
                  <p class="payment-method__name">{{ method.name }}</p>
                  <p class="payment-method__desc">{{ method.description }}</p>
                </div>
              </div>
            </label>
          </div>
        </div>

        <div class="payment-summary">
          <div class="summary-row">
            <span>Montant:</span>
            <strong>{{ form.amount.toLocaleString() }} FCFA</strong>
          </div>
          <div class="summary-row">
            <span>Méthode:</span>
            <strong>{{ paymentMethods.find(m => m.id === form.method)?.name }}</strong>
          </div>
        </div>

        <button type="submit" class="btn-gold modal__submit" :disabled="isProcessing">
          {{ isProcessing ? 'Traitement...' : 'Procéder au Paiement' }}
        </button>

        <p class="modal__disclaimer">
          Votre paiement sera sécurisé. Vous recevrez une confirmation par SMS.
        </p>
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
  from { opacity: 0; }
  to { opacity: 1; }
}

.modal {
  background: var(--color-bg-card);
  border: 1px solid var(--color-border-gold);
  width: 100%;
  max-width: 520px;
  padding: 2.5rem;
  position: relative;
  animation: slideUp 0.3s ease;
  max-height: 90vh;
  overflow-y: auto;
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
}

.modal__form {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 0.6rem;
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

.presets {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 0.6rem;
  margin-top: 0.8rem;
}

.preset-btn {
  background: rgba(201, 168, 76, 0.1);
  border: 1px solid var(--color-border-gold);
  color: var(--color-gold);
  padding: 0.5rem;
  font-size: 0.7rem;
  font-weight: 600;
  cursor: pointer;
  transition: background 0.2s, border-color 0.2s;
}

.preset-btn:hover {
  background: rgba(201, 168, 76, 0.2);
  border-color: var(--color-gold);
}

.payment-methods {
  display: flex;
  flex-direction: column;
  gap: 0.8rem;
}

.payment-method {
  display: flex;
  cursor: pointer;
}

.payment-method__input {
  display: none;
}

.payment-method__content {
  flex: 1;
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 1rem;
  border: 1px solid var(--color-border);
  background: rgba(255, 255, 255, 0.02);
  transition: all 0.2s;
}

.payment-method__input:checked + .payment-method__content {
  border-color: var(--color: var(--color-gold));
  background: rgba(var(--color), 0.1);
}

.payment-method__icon {
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--color: var(--color-gold));
  flex-shrink: 0;
}

.payment-method__text {
  flex: 1;
}

.payment-method__name {
  font-size: 0.85rem;
  font-weight: 600;
  color: var(--color-text);
}

.payment-method__desc {
  font-size: 0.7rem;
  color: var(--color-text-muted);
  margin-top: 0.2rem;
}

.payment-summary {
  background: rgba(201, 168, 76, 0.05);
  border: 1px solid var(--color-border-gold);
  padding: 1rem;
  display: flex;
  flex-direction: column;
  gap: 0.6rem;
}

.summary-row {
  display: flex;
  justify-content: space-between;
  font-size: 0.85rem;
  color: var(--color-text-muted);
}

.summary-row strong {
  color: var(--color-gold);
}

.modal__submit {
  font-size: 0.8rem;
  padding: 0.85rem 1.5rem;
  letter-spacing: 0.15em;
  width: 100%;
  transition: background 0.25s, opacity 0.25s;
  margin-top: 0.5rem;
}

.modal__submit:disabled {
  opacity: 0.7;
  cursor: not-allowed;
}

.modal__disclaimer {
  font-size: 0.7rem;
  color: var(--color-text-subtle);
  text-align: center;
  margin-top: 0.5rem;
}

@media (max-width: 600px) {
  .modal {
    width: 90%;
    max-width: none;
    padding: 2rem 1.5rem;
  }

  .presets {
    grid-template-columns: repeat(3, 1fr);
  }

  .modal__title {
    font-size: 1.2rem;
  }
}
</style>
