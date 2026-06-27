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

const showReservationModal = ref(false)

const openReservation = () => {
  showReservationModal.value = true
}

const closeReservation = () => {
  showReservationModal.value = false
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
  <ReservationModal :is-open="showReservationModal" @close="closeReservation" />
</template>

