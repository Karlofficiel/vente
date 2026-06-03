<script setup lang="ts">
interface Engagement {
  icon: string
  title: string
  description: string
}

const engagements: Engagement[] = [
  {
    icon: 'shield',
    title: 'Sécurité Maximale',
    description: 'Nos chauffeurs formés et certifiés garantissent votre sécurité à chaque kilomètre parcouru.',
  },
  {
    icon: 'eye-off',
    title: 'Sécurité Maximale',
    description: 'Votre vie privée est notre priorité absolue. Discrétion et confidentialité sont nos maîtres mots.',
  },
  {
    icon: 'clock',
    title: 'Sécurité Maximale',
    description: 'Un service de conciergerie voiture coûte tout moment, pour répondre à tous vos besoins.',
  },
]
</script>

<template>
  <section id="engagements" class="engagements">
    <div class="engagements__container">
      <div class="engagements__content">
        <p class="section-label">Nos Engagements</p>
        <div class="gold-divider" style="margin: 0.75rem 0;"></div>
        <h2 class="section-title">L'Excellence Sans Compromis</h2>

        <div class="engagements__list">
          <div v-for="(item, i) in engagements" :key="i" class="engagement-item">
            <div class="engagement-item__number">0{{ i + 1 }}</div>
            <div class="engagement-item__body">
              <div class="engagement-item__icon">
                <svg v-if="item.icon === 'shield'" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/>
                </svg>
                <svg v-else-if="item.icon === 'eye-off'" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M17.94 17.94A10.07 10.07 0 0112 20c-7 0-11-8-11-8a18.45 18.45 0 015.06-5.94M9.9 4.24A9.12 9.12 0 0112 4c7 0 11 8 11 8a18.5 18.5 0 01-2.16 3.19m-6.72-1.07a3 3 0 11-4.24-4.24"/>
                  <line x1="1" y1="1" x2="23" y2="23"/>
                </svg>
                <svg v-else width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <circle cx="12" cy="12" r="10"/><path d="M12 6v6l4 2"/>
                </svg>
              </div>
              <div>
                <h3 class="engagement-item__title">{{ item.title }}</h3>
                <p class="engagement-item__desc">{{ item.description }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="engagements__image-col">
        <img
          src="https://images.pexels.com/photos/3802510/pexels-photo-3802510.jpeg?auto=compress&cs=tinysrgb&w=800"
          alt="Véhicule de prestige"
          class="engagements__img"
        />
        <div class="engagements__img-badge">
          <svg width="36" height="36" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
            <polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"/>
          </svg>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.engagements {
  background: var(--color-bg-section);
  padding: 6rem 2rem;
}

.engagements__container {
  max-width: 1100px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 5rem;
  align-items: center;
}

.engagements__list {
  margin-top: 2.5rem;
  display: flex;
  flex-direction: column;
  gap: 0;
}

.engagement-item {
  display: flex;
  gap: 1.2rem;
  padding: 1.5rem 0;
  border-bottom: 1px solid var(--color-border);
}

.engagement-item:last-child {
  border-bottom: none;
}

.engagement-item__number {
  font-family: 'Playfair Display', serif;
  font-size: 1.6rem;
  color: var(--color-border-gold);
  line-height: 1;
  flex-shrink: 0;
  width: 2.5rem;
}

.engagement-item__body {
  display: flex;
  gap: 0.9rem;
  align-items: flex-start;
}

.engagement-item__icon {
  color: var(--color-gold);
  margin-top: 0.15rem;
  flex-shrink: 0;
}

.engagement-item__title {
  font-family: 'Playfair Display', serif;
  font-size: 1rem;
  color: var(--color-gold);
  margin-bottom: 0.4rem;
}

.engagement-item__desc {
  font-size: 0.85rem;
  color: var(--color-text-muted);
  line-height: 1.7;
}

.engagements__image-col {
  position: relative;
}

.engagements__img {
  width: 100%;
  height: 480px;
  object-fit: cover;
  filter: brightness(0.7);
}

.engagements__img-badge {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 80px;
  height: 80px;
  background: rgba(10,10,10,0.7);
  border: 1px solid var(--color-border-gold);
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--color-gold);
  backdrop-filter: blur(4px);
}

@media (max-width: 900px) {
  .engagements__container {
    grid-template-columns: 1fr;
    gap: 3rem;
  }
  .engagements__image-col { order: -1; }
  .engagements__img { height: 300px; }
}
</style>
