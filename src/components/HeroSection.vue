<script setup lang="ts">
import v1 from "../assets/v1.jpg";
</script>

<template>
  <section id="accueil" class="hero">
    <div class="hero__bg">
      <img
        :src="v1"
        alt="Luxury car"
        class="hero__bg-img"  
      />
      <div class="hero__overlay"></div>
    </div>

    <div class="hero__content">
      <p class="section-label hero__label">Vinita Services</p>
      <h1 class="hero__title">L'Excellence à<br/>Chaque Kilomètre</h1>
      <p class="hero__subtitle">Découvrez le summum du confort urbain avec nos berlines de prestige.</p>
      <a href="#services" class="btn-gold hero__btn">Découvrir</a>
    </div>

    <div class="hero__scroll">
      <div class="hero__scroll-line"></div>
    </div>
  </section>
</template>

<style scoped>
.hero {
  position: relative;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  overflow: hidden;
}

.hero__bg {
  position: absolute;
  inset: 0;
}

.hero__bg-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center 60%;
  filter: brightness(0.45);
}

.hero__overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(
    to bottom,
    rgba(10,10,10,0.3) 0%,
    rgba(10,10,10,0.1) 50%,
    rgba(10,10,10,0.8) 100%
  );
}

.hero__content {
  position: relative;
  z-index: 2;
  max-width: 680px;
  padding: 0 2rem;
  padding-top: 68px;
}

.hero__label {
  margin-bottom: 1.2rem;
}

.hero__title {
  font-size: clamp(2.4rem, 6vw, 4.2rem);
  font-weight: 700;
  color: var(--color-text);
  letter-spacing: -0.01em;
  margin-bottom: 1.2rem;
  line-height: 1.15;
}

.hero__subtitle {
  font-size: 1rem;
  color: rgba(240, 236, 228, 0.7);
  margin-bottom: 2.5rem;
  font-weight: 300;
}

.hero__btn {
  font-size: 0.8rem;
  letter-spacing: 0.2em;
  padding: 0.9rem 2.4rem;
}

.hero__scroll {
  position: absolute;
  bottom: 2.5rem;
  left: 50%;
  transform: translateX(-50%);
  z-index: 2;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.hero__scroll-line {
  width: 1px;
  height: 50px;
  background: linear-gradient(to bottom, var(--color-gold), transparent);
  animation: scrollPulse 2s ease-in-out infinite;
}

@keyframes scrollPulse {
  0%, 100% { opacity: 0.4; transform: scaleY(1); }
  50% { opacity: 1; transform: scaleY(1.15); }
}
</style>
