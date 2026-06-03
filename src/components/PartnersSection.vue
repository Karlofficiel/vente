<script setup lang="ts">
const partners = [
  { name: 'Rolls-Royce', initial: 'RR' },
  { name: 'Bentley', initial: 'B' },
  { name: 'Mercedes', initial: 'MB' },
  { name: 'Range Rover', initial: 'RR' },
]
</script>

<template>
  <section id="partenaires" class="partners">
    <div class="partners__container">
      <div class="partners__header">
        <p class="section-label">Partenaires d'Excellence</p>
        <div class="gold-divider"></div>
        <p class="partners__desc">
          Nous collaborons avec les plus grandes maisons automobiles pour vous offrir le meilleur.
        </p>
        <p class="section-subtitle" style="margin-top: 0.25rem;">Notre Flotte de Prestige</p>
      </div>

      <div class="partners__logos">
        <div v-for="partner in partners" :key="partner.name" class="partners__logo-item">
          <span class="partners__logo-text">{{ partner.name }}</span>
        </div>
      </div>

      <div class="partners__fleet-banner">
        <img
          src="https://images.pexels.com/photos/1638459/pexels-photo-1638459.jpeg?auto=compress&cs=tinysrgb&w=1920"
          alt="Our Premium Fleet"
          class="partners__fleet-img"
        />
        <div class="partners__fleet-overlay">
          <p class="partners__fleet-label">OUR PREMIUM FLEET</p>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.partners {
  background: var(--color-bg-section);
  padding: 6rem 2rem;
}

.partners__container {
  max-width: 1100px;
  margin: 0 auto;
}

.partners__header {
  text-align: center;
  margin-bottom: 3.5rem;
}

.partners__desc {
  font-size: 0.88rem;
  color: var(--color-text-muted);
  margin-top: 1rem;
  max-width: 480px;
  margin-left: auto;
  margin-right: auto;
}

.partners__logos {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 1.5px;
  background: var(--color-border);
  margin-bottom: 3rem;
}

.partners__logo-item {
  background: var(--color-bg-card);
  padding: 1.8rem 3rem;
  display: flex;
  align-items: center;
  justify-content: center;
  min-width: 160px;
  transition: background 0.3s;
}

.partners__logo-item:hover {
  background: #1a1a1a;
}

.partners__logo-text {
  font-family: 'Playfair Display', serif;
  font-size: 1.1rem;
  color: var(--color-text-muted);
  letter-spacing: 0.1em;
  text-transform: uppercase;
  transition: color 0.3s;
}

.partners__logo-item:hover .partners__logo-text {
  color: var(--color-gold);
}

.partners__fleet-banner {
  position: relative;
  height: 300px;
  overflow: hidden;
}

.partners__fleet-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  filter: brightness(0.4);
  transition: transform 0.6s ease;
}

.partners__fleet-banner:hover .partners__fleet-img {
  transform: scale(1.03);
}

.partners__fleet-overlay {
  position: absolute;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: center;
}

.partners__fleet-label {
  font-family: 'Playfair Display', serif;
  font-size: clamp(1.4rem, 4vw, 2.4rem);
  color: var(--color-text);
  letter-spacing: 0.25em;
  text-transform: uppercase;
  border: 1px solid var(--color-border-gold);
  padding: 1rem 2.5rem;
}
</style>
