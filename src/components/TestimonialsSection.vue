<script setup lang="ts">
interface Testimonial {
  stars: number
  text: string
  author: string
}

const testimonials: Testimonial[] = [
  {
    stars: 5,
    text: 'Un service irréprochable. Le chauffeur est ponctuel et le véhicule d\'une propreté exemplaire. Une expérience 5 étoiles.',
    author: 'Jean D.',
  },
  {
    stars: 5,
    text: '"Vinita Services est notre partenaire de confiance pour tous nos transferts. Paris. Discrétion et professionnalisme garantis."',
    author: 'Sarah M.',
  },
  {
    stars: 5,
    text: 'La réservation est simple et rapide. Les chauffeurs sont magnifiques. Je recommande vivement pour vos événements accueil.',
    author: 'Marc L.',
  },
]
</script>

<template>
  <section id="temoignages" class="testimonials">
    <div class="testimonials__container">
      <div class="testimonials__header">
        <p class="section-label">Témoignages Clients</p>
        <div class="gold-divider"></div>
        <p class="section-subtitle">Ils Nous Font Confiance</p>
      </div>

      <div class="testimonials__grid">
        <article v-for="(t, i) in testimonials" :key="i" class="testimonial-card">
          <div class="testimonial-card__stars">
            <svg v-for="s in t.stars" :key="s" width="14" height="14" viewBox="0 0 24 24" fill="currentColor">
              <polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"/>
            </svg>
          </div>
          <p class="testimonial-card__text">{{ t.text }}</p>
          <p class="testimonial-card__author">— {{ t.author }}</p>
        </article>
      </div>
    </div>
  </section>
</template>

<style scoped>
.testimonials {
  background: var(--color-bg);
  padding: 6rem 2rem;
}

.testimonials__container {
  max-width: 1100px;
  margin: 0 auto;
}

.testimonials__header {
  text-align: center;
  margin-bottom: 4rem;
}

.testimonials__grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.5px;
  background: var(--color-border);
}

.testimonial-card {
  background: var(--color-bg-card);
  padding: 2.2rem 1.8rem;
  display: flex;
  flex-direction: column;
  gap: 1.2rem;
  transition: background 0.3s;
}

.testimonial-card:hover {
  background: #1a1a1a;
}

.testimonial-card__stars {
  display: flex;
  gap: 0.2rem;
  color: var(--color-gold);
}

.testimonial-card__text {
  font-size: 0.88rem;
  color: var(--color-text-muted);
  line-height: 1.8;
  flex: 1;
  font-style: italic;
}

.testimonial-card__author {
  font-size: 0.8rem;
  font-weight: 600;
  color: var(--color-text);
  letter-spacing: 0.05em;
}

@media (max-width: 768px) {
  .testimonials__grid {
    grid-template-columns: 1fr;
    gap: 1px;
  }
}
</style>
