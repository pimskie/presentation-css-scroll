<template>
  <div class="slidev-layout kb-cover">
    <div class="kb-cover__comb" aria-hidden="true" />
    <div class="kb-cover__content">
      <slot />
    </div>
    <div class="kb-cover__tape" aria-hidden="true" />
  </div>
</template>

<style scoped>
.kb-cover {
  position: relative;
  display: grid;
  align-content: center;
  overflow: hidden;
}

.kb-cover__comb {
  position: absolute;
  inset: 0;
  background-image: var(--kb-comb);
  background-size: 56px 98px;
  mask-image: radial-gradient(120% 90% at 85% 15%, black 0%, transparent 100%);
}

.kb-cover__content {
  position: relative;
  max-inline-size: 42rem;
}

.kb-cover__content :deep(h1) {
  font-size: 4.6rem;
  line-height: 0.95;
  margin-bottom: 1.75rem;
}

.kb-cover__content :deep(h1 + p) {
  margin-top: 0;
  font-size: 1.2rem;
  color: var(--kb-bone);
}

.kb-cover__tape {
  position: absolute;
  inset-inline: 0;
  bottom: 0;
  height: 0.9rem;
  background: var(--kb-tape);
}
</style>
