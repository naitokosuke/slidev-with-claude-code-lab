<template>
  <div class="slidev-layout thank-you-layout">
    <slot />
  </div>
</template>

<style scoped>
.thank-you-layout {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  padding: 3rem;
  box-sizing: border-box;
  overflow: hidden;
}

/* 深海の特別な背景 - ありがとうスライド用 */
.thank-you-layout::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: 
    radial-gradient(ellipse 100% 80% at 50% 20%, rgba(125, 211, 252, 0.25) 0%, transparent 70%),
    radial-gradient(ellipse 90% 60% at 30% 80%, rgba(167, 243, 208, 0.2) 0%, transparent 60%),
    radial-gradient(ellipse 80% 50% at 70% 50%, rgba(102, 179, 255, 0.15) 0%, transparent 50%),
    linear-gradient(135deg, rgba(10, 14, 39, 0.95) 0%, rgba(26, 40, 86, 0.8) 50%, rgba(45, 74, 125, 0.7) 100%);
  z-index: 1;
  animation: thank-you-glow 6s ease-in-out infinite;
}

/* 波の演出 */
.thank-you-layout::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: 
    linear-gradient(90deg, transparent 0%, rgba(125, 211, 252, 0.3) 50%, transparent 100%),
    linear-gradient(45deg, transparent 0%, rgba(167, 243, 208, 0.2) 50%, transparent 100%),
    linear-gradient(135deg, transparent 0%, rgba(102, 179, 255, 0.25) 50%, transparent 100%);
  background-size: 200% 100%, 300% 100%, 250% 100%;
  animation: thank-you-wave 8s ease-in-out infinite;
  z-index: 2;
  pointer-events: none;
}

@keyframes thank-you-glow {
  0% { 
    transform: translateY(0) translateX(0);
    opacity: 0.9;
  }
  25% { 
    transform: translateY(-8px) translateX(5px);
    opacity: 1;
  }
  50% { 
    transform: translateY(0) translateX(-3px);
    opacity: 0.95;
  }
  75% { 
    transform: translateY(6px) translateX(8px);
    opacity: 1;
  }
  100% { 
    transform: translateY(0) translateX(0);
    opacity: 0.9;
  }
}

@keyframes thank-you-wave {
  0% { 
    background-position: 0% 0%, 0% 0%, 0% 0%;
  }
  50% { 
    background-position: 100% 0%, -50% 0%, 150% 0%;
  }
  100% { 
    background-position: 200% 0%, -100% 0%, 300% 0%;
  }
}

/* コンテンツのz-index */
.thank-you-layout > * {
  position: relative;
  z-index: 10;
}

/* Thank youスライド特有のタイトル強調 */
.thank-you-layout h1 {
  font-size: 5rem !important;
  margin-bottom: 3rem !important;
  text-shadow: 
    0 0 40px rgba(125, 211, 252, 1),
    0 0 80px rgba(125, 211, 252, 0.8),
    0 0 120px rgba(125, 211, 252, 0.6) !important;
  animation: thank-you-title 3s ease-in-out infinite;
}

@keyframes thank-you-title {
  0%, 100% { 
    text-shadow: 
      0 0 40px rgba(125, 211, 252, 1),
      0 0 80px rgba(125, 211, 252, 0.8),
      0 0 120px rgba(125, 211, 252, 0.6);
  }
  50% { 
    text-shadow: 
      0 0 50px rgba(125, 211, 252, 1),
      0 0 100px rgba(125, 211, 252, 0.9),
      0 0 150px rgba(125, 211, 252, 0.7);
  }
}

/* 連絡先情報のスタイル */
.thank-you-layout h2 {
  font-size: 2rem !important;
  margin-bottom: 2rem !important;
  margin-top: 2rem !important;
}

.thank-you-layout p {
  font-size: 1.4rem !important;
  line-height: 2 !important;
  margin-bottom: 1rem !important;
}
</style>