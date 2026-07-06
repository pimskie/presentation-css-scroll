<script setup lang="ts">
import { onMounted, ref } from 'vue';
import IframeUnscaled from '../components/IframeUnscaled.vue';

const props = defineProps<{
  url: string
}>()

const isMounted = ref(false);

onMounted(() => {
  setTimeout(() => {
    isMounted.value = true;
  }, 100);
})

</script>

<template>
  <div class="grid grid-cols-2 w-full h-full">
    <div class="slidev-layout default" v-bind="$attrs">
      <slot />
    </div>
    
    <div relative>
      <IframeUnscaled :src="url" v-if="isMounted" />
    </div>
  </div>
</template>