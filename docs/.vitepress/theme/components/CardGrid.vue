<template>
  <div class="card-grid">
    <slot />
  </div>
</template>

<style scoped>
.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
  gap: 16px;
  margin: 16px 0;
}
</style>
