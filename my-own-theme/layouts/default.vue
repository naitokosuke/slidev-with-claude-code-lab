<template>
  <div class="slidev-layout default-layout">
    <slot />
  </div>
</template>

<style scoped>
.default-layout {
  padding: 2rem;
  width: 100%;
  height: 100%;
  position: relative;
}

/* 深海の光のエフェクト */
.default-layout::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: radial-gradient(
    ellipse at 30% 30%,
    rgba(125, 211, 252, 0.05) 0%,
    transparent 60%
  );
  pointer-events: none;
  z-index: -1;
}
</style>