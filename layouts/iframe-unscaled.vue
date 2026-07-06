<script setup lang="ts">
import { computed } from 'vue'
import IframeUnscaled from '../components/IframeUnscaled.vue';

const props = defineProps<{
  url: string
  scale?: number
}>()

const scaleInvertPercent = computed(() => `${(1 / (props.scale || 1)) * 100}%`)
</script>

<template>
  <div class="iframe-layout">
    <div class="iframe-frame" relative :style="{ width: scaleInvertPercent, height: scaleInvertPercent }">
      <IframeUnscaled
        id="frame" class="w-full h-full"
        :src="url"
      />
    </div>

    <slot />
  </div>
</template>

<style scoped>
/* Padding rondom = klikbare zone om focus terug te geven aan de deck,
   zodat pijltjestoetsen weer werken na interactie met de demo. */
.iframe-layout {
  block-size: 100%;
  inline-size: 100%;
  padding: 2.5rem;
  box-sizing: border-box;
  background: var(--kb-black);
}

.iframe-frame {
  block-size: 100%;
  inline-size: 100%;
  border: 2px solid var(--kb-line);
  border-radius: 0.5rem;
  overflow: hidden;
}
</style>
