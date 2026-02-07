<template>
  <main class="card">
    <slot />
  </main>
</template>

<style scoped>
.card {
  width: min(600px, 100%);
  background: #1e1e1e; /* card dark gray */
  padding: 18px;
  border-radius: 16px;
  box-shadow: 0 10px 24px rgba(0, 0, 0, 0.6);
}
</style>
