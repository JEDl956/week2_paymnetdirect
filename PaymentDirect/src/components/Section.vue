<template>
  <section>
    <h3>{{ title }}</h3>
    <slot />
  </section>
</template>

<script setup>
defineProps({
  title: String
})
</script>

<style scoped>
h3 {
  color: black;
}
</style>
