<template>
  <div class="slidev-layout kb-quote">
    <div class="kb-quote__mark" aria-hidden="true">&ldquo;</div>
    <div class="kb-quote__content">
      <slot />
    </div>
  </div>
</template>

<style scoped>
.kb-quote {
  display: grid;
  align-content: center;
  justify-items: start;
  padding-inline: 6rem;
}

.kb-quote__mark {
  font-family: var(--kb-display);
  font-size: 7rem;
  line-height: 0.5;
  color: var(--kb-honey);
  margin-bottom: 1rem;
}

.kb-quote__content :deep(h1),
.kb-quote__content :deep(h2) {
  text-transform: none;
  font-family: var(--kb-display);
  font-size: 2.6rem;
  line-height: 1.15;
  color: var(--kb-bone);
  margin-bottom: 1.5rem;
}

/* attribution: last paragraph */
.kb-quote__content :deep(p:last-child) {
  color: var(--kb-smoke);
  text-transform: uppercase;
  letter-spacing: 0.12em;
  font-size: 0.85rem;
  font-weight: 600;
}
</style>
