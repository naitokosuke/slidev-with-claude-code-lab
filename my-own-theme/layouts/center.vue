<template>
  <div class="slidev-layout center-layout">
    <slot />
  </div>
</template>

<style scoped>
.center-layout {
  padding: 2rem;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  position: relative;
}

/* 中央に集まる光のエフェクト */
.center-layout::before {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 150%;
  height: 150%;
  background: radial-gradient(
    circle at center,
    rgba(125, 211, 252, 0.08) 0%,
    rgba(102, 179, 255, 0.04) 30%,
    transparent 60%
  );
  border-radius: 50%;
  pointer-events: none;
  z-index: -1;
  animation: gentle-pulse 6s ease-in-out infinite;
}

@keyframes gentle-pulse {
  0%, 100% { opacity: 0.8; transform: translate(-50%, -50%) scale(1); }
  50% { opacity: 1; transform: translate(-50%, -50%) scale(1.05); }
}
</style>