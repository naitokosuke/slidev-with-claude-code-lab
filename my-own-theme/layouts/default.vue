<template>
  <div class="slidev-layout default-layout">
    <slot />
  </div>
</template>

<style scoped>
.default-layout {
  padding: 4rem;
  width: 100%;
  height: 100%;
  position: relative;
  overflow: hidden;
}

/* 深海の層構造で立体感を追加 */
.default-layout::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: 
    radial-gradient(ellipse 60% 40% at 30% 30%, rgba(125, 211, 252, 0.08) 0%, transparent 50%),
    radial-gradient(ellipse 50% 35% at 70% 70%, rgba(102, 179, 255, 0.06) 0%, transparent 45%),
    radial-gradient(ellipse 40% 30% at 50% 80%, rgba(167, 243, 208, 0.04) 0%, transparent 40%);
  pointer-events: none;
  z-index: -1;
  animation: gentle-flow 15s ease-in-out infinite;
}

/* 微細な光の粒子 */
.default-layout::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-image: 
    radial-gradient(circle 1px at 15% 15%, rgba(125, 211, 252, 0.4) 0%, transparent 50%),
    radial-gradient(circle 1px at 85% 25%, rgba(167, 243, 208, 0.3) 0%, transparent 50%),
    radial-gradient(circle 1px at 25% 85%, rgba(102, 179, 255, 0.35) 0%, transparent 50%);
  animation: twinkle 10s ease-in-out infinite;
  pointer-events: none;
  z-index: -1;
}

@keyframes gentle-flow {
  0%, 100% { transform: translateX(0) translateY(0); opacity: 0.7; }
  33% { transform: translateX(-8px) translateY(-4px); opacity: 1; }
  66% { transform: translateX(8px) translateY(4px); opacity: 0.8; }
}

@keyframes twinkle {
  0%, 100% { opacity: 0.3; }
  50% { opacity: 0.8; }
}
</style>
