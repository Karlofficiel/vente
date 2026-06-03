<script setup lang="ts">
import { ref } from 'vue'
import TheNavbar from './components/TheNavbar.vue'
import HeroSection from './components/HeroSection.vue'
import ServicesSection from './components/ServicesSection.vue'
import AboutSection from './components/AboutSection.vue'
import EngagementsSection from './components/EngagementsSection.vue'
import TestimonialsSection from './components/TestimonialsSection.vue'
import PartnersSection from './components/PartnersSection.vue'
import TheFooter from './components/TheFooter.vue'
import ReservationModal from './components/ReservationModal.vue'
import PaymentModal from './components/PaymentModal.vue'

interface ReservationData {
  fullName: string
  email: string
  date: string
  vehicle: string
  message?: string
}

const showReservationModal = ref(false)
const showPaymentModal = ref(false)
const reservationData = ref<ReservationData | null>(null)

const openReservation = () => {
  showReservationModal.value = true
}

const closeReservation = () => {
  showReservationModal.value = false
}

const openPayment = (data: ReservationData) => {
  reservationData.value = data
  showReservationModal.value = false
  showPaymentModal.value = true
}

const closePayment = () => {
  showPaymentModal.value = false
  reservationData.value = null
}
</script>

<template>
  <TheNavbar @open-reservation="openReservation" />
  <main>
    <HeroSection @open-reservation="openReservation" />
    <ServicesSection @open-reservation="openReservation" />
    <AboutSection />
    <EngagementsSection />
    <TestimonialsSection />
    <PartnersSection />
  </main>
  <TheFooter />
  <ReservationModal :is-open="showReservationModal" @close="closeReservation" @open-payment="openPayment" />
  <PaymentModal :is-open="showPaymentModal" :reservation-data="reservationData" @close="closePayment" />
</template>
