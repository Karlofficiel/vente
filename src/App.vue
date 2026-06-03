<script setup lang="ts">
import TheNavbar from './components/TheNavbar.vue'
import HeroSection from './components/HeroSection.vue'
import ServicesSection from './components/ServicesSection.vue'
import AboutSection from './components/AboutSection.vue'
import EngagementsSection from './components/EngagementsSection.vue'
import TestimonialsSection from './components/TestimonialsSection.vue'
import PartnersSection from './components/PartnersSection.vue'
import TheFooter from './components/TheFooter.vue'
</script>

<template>
  <TheNavbar />
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
