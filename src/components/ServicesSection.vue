<script setup lang="ts">
interface Service {
  icon: string
  title: string
  description: string
}

const services: Service[] = [
  {
    icon: 'car',
    title: 'Berlines de Luxe',
    description: 'Le raffinement ultime pour vos rendez-vous d\'affaires. Alliez prestige et confort technologique pour des trajets sereins.',
  },
  {
    icon: 'suv',
    title: 'SUV Premium',
    description: 'L\'espace et la puissance sans compromis sur le luxe. Idéal pour vos escapades en famille ou vos trajets vers les stations.',
  },
  {
    icon: 'vip',
    title: 'Transferts VIP',
    description: 'Service de chauffeur privé 24h/24. Discrétion, ponctualité et accueil personnalisé pour tous vos déplacements.',
  },
]
</script>

<template>
  <section id="services" class="services">
    <div class="services__container">
      <div class="services__header">
        <p class="section-label">Nos Services</p>
        <div class="gold-divider"></div>
        <p class="section-subtitle">Luxueux de Véhicules d'Exception</p>
      </div>

      <div class="services__grid">
        <article v-for="service in services" :key="service.title" class="service-card">
          <div class="service-card__icon">
            <svg v-if="service.icon === 'car'" width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
              <path d="M5 17H3a2 2 0 01-2-2v-4a2 2 0 011-1.73l4-2.31A4 4 0 019.38 6h5.24a4 4 0 013.38 1.96l4 2.31A2 2 0 0123 12v3a2 2 0 01-2 2h-2"/>
              <circle cx="7.5" cy="17.5" r="2.5"/><circle cx="16.5" cy="17.5" r="2.5"/>
            </svg>
            <svg v-else-if="service.icon === 'suv'" width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
              <rect x="1" y="8" width="22" height="10" rx="2"/><path d="M4 8V6a2 2 0 012-2h12a2 2 0 012 2v2"/>
              <circle cx="7" cy="18" r="2"/><circle cx="17" cy="18" r="2"/>
            </svg>
            <svg v-else width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
              <path d="M12 2L2 7l10 5 10-5-10-5z"/><path d="M2 17l10 5 10-5"/><path d="M2 12l10 5 10-5"/>
            </svg>
          </div>

          <h3 class="service-card__title">{{ service.title }}</h3>
          <p class="service-card__desc">{{ service.description }}</p>
          <a href="#reserver" class="service-card__link">
            En savoir plus
            <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <path d="M5 12h14M12 5l7 7-7 7"/>
            </svg>
          </a>
        </article>
      </div>
    </div>
  </section>
</template>

<style scoped>
.services {
  background: var(--color-bg-section);
  padding: 6rem 2rem;
}

.services__container {
  max-width: 1100px;
  margin: 0 auto;
}

.services__header {
  text-align: center;
  margin-bottom: 4rem;
}

.services__grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.5px;
  background: var(--color-border);
}

.service-card {
  background: var(--color-bg-card);
  padding: 2.5rem 2rem;
  transition: background 0.3s;
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.service-card:hover {
  background: #1a1a1a;
}

.service-card__icon {
  color: var(--color-gold);
  width: 52px;
  height: 52px;
  border: 1px solid var(--color-border-gold);
  display: flex;
  align-items: center;
  justify-content: center;
  transition: border-color 0.3s;
}

.service-card:hover .service-card__icon {
  border-color: var(--color-gold);
}

.service-card__title {
  font-family: 'Playfair Display', serif;
  font-size: 1.15rem;
  color: var(--color-text);
}

.service-card__desc {
  font-size: 0.88rem;
  color: var(--color-text-muted);
  line-height: 1.7;
  flex: 1;
}

.service-card__link {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  font-size: 0.75rem;
  font-weight: 600;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--color-gold);
  transition: gap 0.2s;
}

.service-card__link:hover {
  gap: 0.8rem;
}

@media (max-width: 768px) {
  .services__grid {
    grid-template-columns: 1fr;
    gap: 1px;
  }
}
</style>
