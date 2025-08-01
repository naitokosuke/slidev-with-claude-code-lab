<template>
  <div class="slidev-layout center-page">
    <div class="center-content">
      <slot />
    </div>
  </div>
</template>

<style>
.center-page {
  width: 100%;
  height: 100%;
  position: relative;
  overflow: hidden;
  display: table;
}

.center-content {
  display: table-cell;
  vertical-align: middle;
  text-align: center;
}

/* 深海の層構造で立体感を追加 */
.center-page::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: 
    radial-gradient(ellipse 80% 50% at 50% 30%, rgba(125, 211, 252, 0.15) 0%, transparent 50%),
    radial-gradient(ellipse 60% 40% at 30% 70%, rgba(102, 179, 255, 0.1) 0%, transparent 40%),
    radial-gradient(ellipse 70% 35% at 70% 60%, rgba(167, 243, 208, 0.08) 0%, transparent 35%);
  pointer-events: none;
  z-index: 1;
  animation: deep-flow 8s ease-in-out infinite;
}

/* 泡のエフェクト */
.center-page::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-image: 
    radial-gradient(circle 3px at 20% 80%, rgba(125, 211, 252, 0.6) 0%, transparent 50%),
    radial-gradient(circle 2px at 80% 20%, rgba(167, 243, 208, 0.5) 0%, transparent 50%),
    radial-gradient(circle 4px at 60% 90%, rgba(102, 179, 255, 0.4) 0%, transparent 50%);
  animation: bubble-float 12s linear infinite;
  pointer-events: none;
  z-index: 1;
}

@keyframes deep-flow {
  0%, 100% { 
    transform: translateX(0) translateY(0) rotate(0deg);
    opacity: 0.8;
  }
  33% { 
    transform: translateX(-10px) translateY(-5px) rotate(1deg);
    opacity: 1;
  }
  66% { 
    transform: translateX(10px) translateY(5px) rotate(-1deg);
    opacity: 0.9;
  }
}

@keyframes bubble-float {
  0% { transform: translateY(100%) scale(0.8); opacity: 0; }
  10% { opacity: 1; }
  90% { opacity: 1; }
  100% { transform: translateY(-100%) scale(1.2); opacity: 0; }
}

/* コンテンツのz-index */
.center-content {
  position: relative;
  z-index: 10;
}
</style>
