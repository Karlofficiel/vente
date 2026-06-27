<script setup lang="ts">
const quickLinks = [
  { label: 'Accueil', href: '#accueil' },
  { label: 'Nos Services', href: '#services' },
  { label: 'À Propos', href: '#apropos' },
  { label: 'Réserver', href: '#reserver' },
  { label: 'Nos Engagements', href: '#engagements' },
  { label: 'Témoignages', href: '#temoignages' },
  { label: 'Partenaires', href: '#partenaires' },
]

const socials = [
  { label: 'Facebook', icon: 'f' },
  { label: 'Instagram', icon: 'in' },
  { label: 'X', icon: 'x' },
]
</script>

<template>
  <footer class="footer">
    <div class="footer__main">
      <div class="footer__brand">
        <div class="footer__logo">
          <span class="footer__logo-icon">VS</span>
          <span class="footer__logo-text">Vinita Services</span>
        </div>
        <p class="footer__tagline">
          L'excellence du transport privé sur mesure. Redéfinir votre standard de voyage avec prestige.
        </p>
      </div>

      <div class="footer__col">
        <p class="footer__col-title">Liens Rapides</p>
        <ul class="footer__links">
          <li v-for="link in quickLinks" :key="link.href">
            <a :href="link.href" class="footer__link">{{ link.label }}</a>
          </li>
        </ul>
      </div>

      <div class="footer__col">
        <p class="footer__col-title">Contact</p>
        <ul class="footer__contact-list">
          <li>
            <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0118 0z"/><circle cx="12" cy="10" r="3"/>
            </svg>
            <span> Garde four en face de l'ecole des Sapeurs Pompiers Terminus , Douala Cameroun</span>
          </li>
          <li>
            <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <path d="M22 16.92v3a2 2 0 01-2.18 2 19.79 19.79 0 01-8.63-3.07A19.5 19.5 0 013.07 9.68 19.79 19.79 0 01.03 1.05 2 2 0 012 0h3a2 2 0 012 1.72c.127.96.361 1.903.7 2.81a2 2 0 01-.45 2.11L6.11 7.82a16 16 0 006.06 6.06l1.18-1.18a2 2 0 012.11-.45c.907.339 1.85.573 2.81.7A2 2 0 0122 14.92z"/>
            </svg>
            <span>+237 699 82 02 63</span>
          </li>
          <li>
            <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/>
            </svg>
            <span>vinitaservicessarl@gmail.com</span>
          </li>
        </ul>
      </div>

      <div class="footer__col">
        <p class="footer__col-title">Suivez-Nous</p>
        <div class="footer__socials">
          <a v-for="s in socials" :key="s.label" href="#" class="footer__social" :aria-label="s.label">
            {{ s.icon }}
          </a>
        </div>
      </div>
    </div>

    <div class="footer__bottom">
      <p>© 2026 Vinita Services. Tous droits réservés.</p>
      <div class="footer__bottom-links">
        <a href="#">Politique de Confidentialité</a>
        <a href="#">Conditions d'Utilisation</a>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  background: #080808;
  border-top: 1px solid var(--color-border);
}

.footer__main {
  max-width: 1100px;
  margin: 0 auto;
  padding: 4rem 2rem;
  display: grid;
  grid-template-columns: 2fr 1fr 1.5fr 1fr;
  gap: 3rem;
}

.footer__logo {
  display: flex;
  align-items: center;
  gap: 0.6rem;
  margin-bottom: 1.2rem;
}

.footer__logo-icon {
  width: 32px;
  height: 32px;
  border: 1.5px solid var(--color-gold);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.6rem;
  font-weight: 700;
  color: var(--color-gold);
  letter-spacing: 0.05em;
}

.footer__logo-text {
  font-family: 'Playfair Display', serif;
  font-size: 0.95rem;
  color: var(--color-text);
}

.footer__tagline {
  font-size: 0.82rem;
  color: var(--color-text-muted);
  line-height: 1.8;
}

.footer__col-title {
  font-size: 0.7rem;
  font-weight: 600;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--color-gold);
  margin-bottom: 1.2rem;
}

.footer__links {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 0.6rem;
}

.footer__link {
  font-size: 0.82rem;
  color: var(--color-text-muted);
  transition: color 0.2s;
}

.footer__link:hover {
  color: var(--color-gold);
}

.footer__contact-list {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 0.8rem;
}

.footer__contact-list li {
  display: flex;
  align-items: flex-start;
  gap: 0.6rem;
  font-size: 0.82rem;
  color: var(--color-text-muted);
  line-height: 1.5;
}

.footer__contact-list svg {
  color: var(--color-gold);
  flex-shrink: 0;
  margin-top: 0.15rem;
}

.footer__socials {
  display: flex;
  gap: 0.6rem;
}

.footer__social {
  width: 34px;
  height: 34px;
  border: 1px solid var(--color-border);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.7rem;
  font-weight: 700;
  color: var(--color-text-muted);
  text-transform: uppercase;
  transition: border-color 0.2s, color 0.2s;
}

.footer__social:hover {
  border-color: var(--color-gold);
  color: var(--color-gold);
}

.footer__bottom {
  max-width: 1100px;
  margin: 0 auto;
  padding: 1.5rem 2rem;
  border-top: 1px solid var(--color-border);
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
  flex-wrap: wrap;
}

.footer__bottom p,
.footer__bottom a {
  font-size: 0.75rem;
  color: var(--color-text-subtle);
}

.footer__bottom-links {
  display: flex;
  gap: 1.5rem;
}

.footer__bottom-links a:hover {
  color: var(--color-text-muted);
}

@media (max-width: 900px) {
  .footer__main {
    grid-template-columns: 1fr 1fr;
    gap: 2rem;
  }
  .footer__brand { grid-column: 1 / -1; }
}

@media (max-width: 500px) {
  .footer__main { grid-template-columns: 1fr; }
}
</style>
