<template>
  <div
    v-if="$slidev.nav.currentPage > 1"
    class="kb-hex-badge"
  >
    {{ $slidev.nav.currentPage }}
  </div>
</template>
