<template>
  <div class="slidev-layout section-layout">
    <slot />
  </div>
</template>

<style scoped>
.section-layout {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  position: relative;
  overflow: hidden;
  padding: 3rem;
}

/* 深海の深層背景 - 複数レイヤーで立体感 */
.section-layout::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: 
    linear-gradient(135deg, rgba(10, 14, 39, 0.9) 0%, rgba(26, 40, 86, 0.7) 50%, rgba(45, 74, 125, 0.5) 100%),
    radial-gradient(ellipse 100% 60% at 50% 40%, rgba(125, 211, 252, 0.15) 0%, transparent 60%),
    radial-gradient(ellipse 80% 50% at 20% 80%, rgba(102, 179, 255, 0.1) 0%, transparent 50%),
    radial-gradient(ellipse 70% 40% at 80% 20%, rgba(167, 243, 208, 0.08) 0%, transparent 40%);
  z-index: 1;
  animation: deep-current 20s ease-in-out infinite;
}

/* 光の粒子エフェクト */
.section-layout::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-image: 
    radial-gradient(circle 2px at 25% 25%, rgba(125, 211, 252, 0.8) 0%, transparent 50%),
    radial-gradient(circle 3px at 75% 75%, rgba(167, 243, 208, 0.6) 0%, transparent 50%),
    radial-gradient(circle 1px at 50% 10%, rgba(102, 179, 255, 0.7) 0%, transparent 50%),
    radial-gradient(circle 2px at 10% 90%, rgba(125, 211, 252, 0.5) 0%, transparent 50%);
  animation: sparkle 8s ease-in-out infinite;
  z-index: 2;
  pointer-events: none;
}

@keyframes deep-current {
  0%, 100% { 
    transform: translateX(0) translateY(0) scale(1);
    opacity: 0.8;
  }
  25% { 
    transform: translateX(-15px) translateY(-8px) scale(1.02);
    opacity: 1;
  }
  50% { 
    transform: translateX(0) translateY(-12px) scale(0.98);
    opacity: 0.9;
  }
  75% { 
    transform: translateX(15px) translateY(-5px) scale(1.01);
    opacity: 0.95;
  }
}

@keyframes sparkle {
  0%, 100% { opacity: 0.6; transform: scale(1); }
  25% { opacity: 1; transform: scale(1.2); }
  50% { opacity: 0.8; transform: scale(0.9); }
  75% { opacity: 1; transform: scale(1.1); }
}
</style>