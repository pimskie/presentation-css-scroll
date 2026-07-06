<template>
  <div class="slidev-layout kb-section">
    <div class="kb-section__comb" aria-hidden="true" />
    <div class="kb-section__content">
      <slot />
    </div>
  </div>
</template>

<style scoped>
/* inverted: black on stinger yellow */
.kb-section {
  position: relative;
  display: grid;
  align-content: center;
  background: var(--kb-honey);
  color: var(--kb-black);
  overflow: hidden;
}

.kb-section__comb {
  position: absolute;
  inset: 0;
  background-image: var(--kb-comb);
  background-size: 56px 98px;
  filter: invert(1) brightness(0.2);
  mask-image: radial-gradient(110% 100% at 15% 85%, black 0%, transparent 60%);
}

.kb-section__content {
  position: relative;
}

.kb-section__content :deep(h1) {
  color: var(--kb-black);
  font-size: 4rem;
  line-height: 0.95;
  margin-bottom: 1rem;
}

.kb-section__content :deep(h1 + p) {
  margin-top: 0;
  color: color-mix(in srgb, var(--kb-black) 70%, var(--kb-honey));
  font-weight: 600;
}

.kb-section__content :deep(.kicker) {
  color: var(--kb-blood);
}

.kb-section__content :deep(strong) {
  color: var(--kb-blood);
}

.kb-section__content :deep(a) {
  color: var(--kb-black);
  border-color: var(--kb-black);
}
</style>
