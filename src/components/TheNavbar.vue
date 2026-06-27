<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

// Déclaration de l'événement pour ouvrir la réservation
const emit = defineEmits<{
  (e: 'open-reservation'): void
}>()

const scrolled = ref(false)
const menuOpen = ref(false)

const navLinks = [
  { label: 'Accueil', href: '#accueil' },
  { label: 'Services', href: '#services' },
  { label: 'À Propos', href: '#apropos' },
  { label: 'Engagements', href: '#engagements' },
  { label: 'Témoignages', href: '#temoignages' },
  { label: 'Partenaires', href: '#partenaires' },
]

function handleScroll() {
  scrolled.value = window.scrollY > 40
}

onMounted(() => window.addEventListener('scroll', handleScroll))
onUnmounted(() => window.removeEventListener('scroll', handleScroll))
</script>

<template>
  <header :class="['navbar', { 'navbar--scrolled': scrolled }]">
    <div class="navbar__inner">
      <a href="#accueil" class="navbar__logo">
        <span class="navbar__logo-icon">VS</span>
        <span class="navbar__logo-text">Vinita Services</span>
      </a>

      <div class="navbar__phone">
        <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <path d="M22 16.92v3a2 2 0 01-2.18 2 19.79 19.79 0 01-8.63-3.07A19.5 19.5 0 013.07 9.68 19.79 19.79 0 01.03 1.05 2 2 0 012 0h3a2 2 0 012 1.72c.127.96.361 1.903.7 2.81a2 2 0 01-.45 2.11L6.11 7.82a16 16 0 006.06 6.06l1.18-1.18a2 2 0 012.11-.45c.907.339 1.85.573 2.81.7A2 2 0 0122 14.92z"/>
        </svg>
        <span>+237 699 82 02 63</span>
      </div>

      <nav class="navbar__nav" :class="{ 'navbar__nav--open': menuOpen }">
        <a
          v-for="link in navLinks"
          :key="link.href"
          :href="link.href"
          class="navbar__link"
          @click="menuOpen = false"
        >{{ link.label }}</a>
        
        <button 
          type="button" 
          class="btn-gold navbar__cta" 
          @click="emit('open-reservation'); menuOpen = false"
        >
          Réserver
        </button>
      </nav>

      <button class="navbar__burger" :class="{ open: menuOpen }" @click="menuOpen = !menuOpen" aria-label="Menu">
        <span></span><span></span><span></span>
      </button>
    </div>
  </header>
</template>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 100;
  transition: background 0.35s, box-shadow 0.35s;
  background: transparent;
}

.navbar--scrolled {
  background: rgba(10, 10, 10, 0.97);
  box-shadow: 0 1px 0 var(--color-border-gold);
}

.navbar__inner {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 2rem;
  height: 68px;
  display: flex;
  align-items: center;
  gap: 2rem;
}

.navbar__logo {
  display: flex;
  align-items: center;
  gap: 0.6rem;
  text-decoration: none;
  flex-shrink: 0;
}

.navbar__logo-icon {
  width: 34px;
  height: 34px;
  border: 1.5px solid var(--color-gold);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.65rem;
  font-weight: 700;
  letter-spacing: 0.05em;
  color: var(--color-gold);
}

.navbar__logo-text {
  font-family: 'Playfair Display', serif;
  font-size: 1rem;
  color: var(--color-text);
  white-space: nowrap;
}

.navbar__phone {
  display: flex;
  align-items: center;
  gap: 0.4rem;
  font-size: 0.78rem;
  color: var(--color-gold);
  margin-right: auto;
}

.navbar__nav {
  display: flex;
  align-items: center;
  gap: 1.6rem;
}

.navbar__link {
  font-size: 0.8rem;
  font-weight: 400;
  letter-spacing: 0.05em;
  color: var(--color-text);
  text-transform: uppercase;
  transition: color 0.2s;
  white-space: nowrap;
}

.navbar__link:hover {
  color: var(--color-gold);
}

.navbar__cta {
  font-size: 0.72rem;
  padding: 0.6rem 1.4rem;
  letter-spacing: 0.12em;
  cursor: pointer;
}

.navbar__burger {
  display: none;
  flex-direction: column;
  gap: 5px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 4px;
  margin-left: auto;
}

.navbar__burger span {
  display: block;
  width: 24px;
  height: 1.5px;
  background: var(--color-text);
  transition: transform 0.3s, opacity 0.3s;
}

.navbar__burger.open span:nth-child(1) { transform: translateY(6.5px) rotate(45deg); }
.navbar__burger.open span:nth-child(2) { opacity: 0; }
.navbar__burger.open span:nth-child(3) { transform: translateY(-6.5px) rotate(-45deg); }

@media (max-width: 960px) {
  .navbar__phone { display: none; }
  .navbar__burger { display: flex; }
  .navbar__nav {
    display: none;
    position: fixed;
    inset: 68px 0 0 0;
    background: rgba(10,10,10,0.98);
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 2rem;
  }
  .navbar__nav--open { display: flex; }
  .navbar__link { font-size: 1rem; }
}
</style>
