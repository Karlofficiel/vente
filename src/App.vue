<script setup lang="ts">
import { ref } from 'vue'
import TheNavbar from './components/TheNavbar.vue'
<<<<<<< HEAD
import ReservationModal from './components/ReservationModal.vue'
=======
>>>>>>> fac89632a9f0b4dec53fbc7388e5245151af4bd4
import HeroSection from './components/HeroSection.vue'
import ServicesSection from './components/ServicesSection.vue'
import AboutSection from './components/AboutSection.vue'
import EngagementsSection from './components/EngagementsSection.vue'
import TestimonialsSection from './components/TestimonialsSection.vue'
import PartnersSection from './components/PartnersSection.vue'
import TheFooter from './components/TheFooter.vue'
<<<<<<< HEAD

const reservationOpen = ref(false)

const openReservation = () => {
  reservationOpen.value = true
}

const closeReservation = () => {
  reservationOpen.value = false
=======
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
>>>>>>> fac89632a9f0b4dec53fbc7388e5245151af4bd4
}
</script>

<template>
<<<<<<< HEAD
  <TheNavbar @openReservation="openReservation" />
  <ReservationModal :isOpen="reservationOpen" @close="closeReservation" />
  <main>
    <HeroSection />
    <ServicesSection />
=======
  <TheNavbar @open-reservation="openReservation" />
  <main>
    <HeroSection @open-reservation="openReservation" />
    <ServicesSection @open-reservation="openReservation" />
>>>>>>> fac89632a9f0b4dec53fbc7388e5245151af4bd4
    <AboutSection />
    <EngagementsSection />
    <TestimonialsSection />
    <PartnersSection />
  </main>
  <TheFooter />
<<<<<<< HEAD
=======
  <ReservationModal :is-open="showReservationModal" @close="closeReservation" @open-payment="openPayment" />
  <PaymentModal :is-open="showPaymentModal" :reservation-data="reservationData" @close="closePayment" />
>>>>>>> fac89632a9f0b4dec53fbc7388e5245151af4bd4
</template>
