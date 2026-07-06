<script setup lang="ts">
import IframeUnscaled from '../components/IframeUnscaled.vue';

const props = defineProps<{
  url: string
}>()

</script>

<template>
  <div class="grid grid-cols-2 w-full h-full">
    <div relative>
      <IframeUnscaled :src="url" />
    </div>
    <div class="slidev-layout default" v-bind="$attrs">
      <slot />
    </div>
  </div>
</template>