<script setup lang="ts">
const stats = [
  { value: '10+', label: "Années d'Excellence" },
  { value: '5000+', label: 'Clients Satisfaits' },
]

const badges = [
  { icon: 'shield', label: 'Confiance', sub: 'Qualité certifiée.' },
  { icon: 'star', label: 'Prestige', sub: 'Qualité à toutes.' },
]
</script>

<template>
  <section id="apropos" class="about">
    <div class="about__container">
      <div class="about__image-col">
        <div class="about__img-wrap">
          <img
            src="https://images.pexels.com/photos/7144212/pexels-photo-7144212.jpeg?auto=compress&cs=tinysrgb&w=800"
            alt="Chauffeur professionnel"
            class="about__img"
          />
          <div class="about__stat-badge">
            <span class="about__stat-value">{{ stats[0].value }}</span>
            <span class="about__stat-label">{{ stats[0].label }}</span>
          </div>
        </div>
      </div>

      <div class="about__content">
        <p class="section-label">À Propos de Nous</p>
        <div class="gold-divider" style="margin: 0.75rem 0;"></div>
        <h2 class="section-title">Une Passion pour l'Exceptionnel</h2>
        <p class="about__text">
          Fondée sur une passion pour l'automobile d'exception, Vinita Services
          est née de la volonté d'offrir plus qu'un simple trajet : une expérience
          sensorielle unique. Depuis plus de 10 ans, nous accompagnons les
          dirigeants les plus exigeants avec une flotte rigoureusement
          sélectionnée et un service d'une discrétion absolue.
        </p>

        <div class="about__badges">
          <div v-for="badge in badges" :key="badge.label" class="about__badge">
            <div class="about__badge-icon">
              <svg v-if="badge.icon === 'shield'" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/>
              </svg>
              <svg v-else width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"/>
              </svg>
            </div>
            <div>
              <p class="about__badge-label">{{ badge.label }}</p>
              <p class="about__badge-sub">{{ badge.sub }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.about {
  background: var(--color-bg);
  padding: 6rem 2rem;
}

.about__container {
  max-width: 1100px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 5rem;
  align-items: center;
}

.about__image-col {
  position: relative;
}

.about__img-wrap {
  position: relative;
}

.about__img {
  width: 100%;
  height: 500px;
  object-fit: cover;
  object-position: center top;
  filter: brightness(0.85);
}

.about__stat-badge {
  position: absolute;
  bottom: -1.5rem;
  right: -1.5rem;
  background: var(--color-bg-card);
  border: 1px solid var(--color-border-gold);
  padding: 1.2rem 1.6rem;
  text-align: center;
}

.about__stat-value {
  display: block;
  font-family: 'Playfair Display', serif;
  font-size: 2rem;
  color: var(--color-gold);
  line-height: 1;
}

.about__stat-label {
  font-size: 0.7rem;
  color: var(--color-text-muted);
  letter-spacing: 0.1em;
  text-transform: uppercase;
  margin-top: 0.3rem;
}

.about__content {
  padding-left: 1rem;
}

.about__text {
  font-size: 0.92rem;
  color: var(--color-text-muted);
  line-height: 1.85;
  margin: 1.5rem 0 2rem;
}

.about__badges {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.about__badge {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 0.9rem 1.2rem;
  border: 1px solid var(--color-border);
  background: var(--color-bg-card);
  transition: border-color 0.3s;
}

.about__badge:hover {
  border-color: var(--color-border-gold);
}

.about__badge-icon {
  color: var(--color-gold);
  flex-shrink: 0;
}

.about__badge-label {
  font-size: 0.85rem;
  font-weight: 600;
  color: var(--color-text);
}

.about__badge-sub {
  font-size: 0.75rem;
  color: var(--color-text-muted);
  margin-top: 0.15rem;
}

@media (max-width: 900px) {
  .about__container {
    grid-template-columns: 1fr;
    gap: 3rem;
  }
  .about__stat-badge {
    right: 1rem;
    bottom: 1rem;
  }
  .about__content { padding-left: 0; }
}
</style>
