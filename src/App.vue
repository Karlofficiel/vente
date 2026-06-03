<script setup lang="ts">
import { ref } from 'vue'
import TheNavbar from './components/TheNavbar.vue'
import ReservationModal from './components/ReservationModal.vue'
import HeroSection from './components/HeroSection.vue'
import ServicesSection from './components/ServicesSection.vue'
import AboutSection from './components/AboutSection.vue'
import EngagementsSection from './components/EngagementsSection.vue'
import TestimonialsSection from './components/TestimonialsSection.vue'
import PartnersSection from './components/PartnersSection.vue'
import TheFooter from './components/TheFooter.vue'

const reservationOpen = ref(false)

const openReservation = () => {
  reservationOpen.value = true
}

const closeReservation = () => {
  reservationOpen.value = false
}
</script>

<template>
  <TheNavbar @openReservation="openReservation" />
  <ReservationModal :isOpen="reservationOpen" @close="closeReservation" />
  <main>
    <HeroSection />
    <ServicesSection />
    <AboutSection />
    <EngagementsSection />
    <TestimonialsSection />
    <PartnersSection />
  </main>
  <TheFooter />
</template>
