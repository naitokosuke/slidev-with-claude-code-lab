<template>
  <div class="slidev-layout section-layout">
    <div class="deep-sea-section">
      <div class="section-background"></div>
      <div class="section-content">
        <slot />
      </div>
    </div>
  </div>
</template>

<style scoped>
.section-layout {
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  overflow: hidden;
}

.deep-sea-section {
  position: relative;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.section-background {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(
    45deg,
    rgba(10, 14, 39, 0.8) 0%,
    rgba(26, 40, 86, 0.6) 50%,
    rgba(45, 74, 125, 0.4) 100%
  );
  z-index: -2;
}

.section-background::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-image: 
    radial-gradient(circle at 30% 20%, rgba(125, 211, 252, 0.2) 0%, transparent 50%),
    radial-gradient(circle at 70% 80%, rgba(167, 243, 208, 0.15) 0%, transparent 50%);
  animation: deep-current 15s ease-in-out infinite;
}

.section-content {
  text-align: center;
  max-width: 80%;
  position: relative;
  z-index: 1;
}

.section-layout h1 {
  font-size: 5rem;
  margin: 0;
  text-shadow: 
    0 0 20px rgba(125, 211, 252, 0.6),
    0 0 40px rgba(125, 211, 252, 0.4),
    0 0 60px rgba(125, 211, 252, 0.2);
  animation: section-glow 3s ease-in-out infinite;
}

.section-layout h2 {
  font-size: 2.5rem;
  margin-top: 1rem;
  color: var(--deep-sea-light);
}

@keyframes deep-current {
  0%, 100% { 
    transform: translateX(0) translateY(0);
    opacity: 0.6;
  }
  33% { 
    transform: translateX(-20px) translateY(-10px);
    opacity: 0.8;
  }
  66% { 
    transform: translateX(20px) translateY(10px);
    opacity: 0.7;
  }
}

@keyframes section-glow {
  0%, 100% { text-shadow: 0 0 20px rgba(125, 211, 252, 0.6); }
  50% { text-shadow: 0 0 30px rgba(125, 211, 252, 0.8), 0 0 60px rgba(125, 211, 252, 0.4); }
}
</style>