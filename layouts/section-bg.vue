<!-- layouts/section-bg.vue -->
<template>
  <div class="slidev-layout section-bg">
    <div class="bg-image absolute top-0 left-0 w-full h-full" :style="{
      backgroundImage: `url(${image})`,
      opacity: backgroundOpacity / 100
    }"></div>
    <div class="content-wrapper relative z-10 flex flex-col justify-center items-center h-full">
      <h1><slot></slot></h1>
    </div>
  </div>
</template>

<script setup>
defineProps({
  image: {
    type: String,
    default: ''
  },
  backgroundOpacity: {
    type: Number,
    default: 100
  },
  overlayOpacity: {
    type: Number,
    default: 50
  },
  textColor: {
    type: String,
    default: 'var(--slidev-theme-primary)'
  }
})
</script>

<style scoped>
.section-bg {
  padding: 0;
}

.bg-image {
  background-size: cover;
  background-position: center;
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.bg-image::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(255, 255, 255, v-bind('overlayOpacity / 100'));
}

h1 {
  color: v-bind('textColor');
  font-size: 4rem;
  font-weight: 600;
  text-align: center;
  /* text-shadow: 0 2px 10px rgba(0, 0, 0, 0.5); */
}
</style>