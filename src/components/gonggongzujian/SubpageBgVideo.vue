<template>
  <div class="subpage-bg-video" aria-hidden="true">
    <div class="fallback-bg"></div>
    <video 
      class="video-element" 
      :class="{ 'is-hidden': showFallback }"
      autoplay 
      loop 
      muted 
      playsinline 
      :src="src"
      @error="handleVideoError"
    ></video>
    <div class="video-overlay"></div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

defineProps({
  src: {
    type: String,
    required: true,
  },
})

const showFallback = ref(false)

const handleVideoError = () => {
  showFallback.value = true
}
</script>

<style scoped>
.subpage-bg-video {
  position: fixed;
  inset: 0;
  z-index: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
  pointer-events: none;
  background: #0a0a0a;
}

.fallback-bg {
  position: absolute;
  inset: 0;
  background:
    radial-gradient(circle at 20% 20%, rgba(200, 168, 102, 0.15), transparent 40%),
    radial-gradient(circle at 80% 80%, rgba(200, 168, 102, 0.08), transparent 35%),
    radial-gradient(circle at 50% 50%, rgba(255, 255, 255, 0.02), transparent 60%),
    linear-gradient(135deg, #0a0a0a 0%, #121212 50%, #0d0d0d 100%);
  pointer-events: none;
}

.video-element {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  opacity: 0.38;
  transition: opacity 0.5s ease;
}

.video-element.is-hidden {
  opacity: 0;
  pointer-events: none;
}

.video-overlay {
  position: absolute;
  inset: 0;
  background:
    radial-gradient(circle at 12% 0%, rgba(255, 255, 255, 0.03), transparent 30%),
    radial-gradient(circle at 88% 8%, rgba(255, 255, 255, 0.015), transparent 34%),
    linear-gradient(180deg, rgba(0, 0, 0, 0.5) 0%, rgba(0, 0, 0, 0.15) 38%, rgba(0, 0, 0, 0.8) 100%);
  pointer-events: none;
}

@media (prefers-reduced-motion: reduce) {
  .video-element {
    display: none;
  }
}
</style>
