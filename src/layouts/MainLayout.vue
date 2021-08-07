<template>
  <main class="main-layout my-5 mx-auto box">
    <slot />
  </main>
</template>

<script>
export default {
name: "MainLayout"
}
</script>

<style scoped>
.main-layout {
  max-width: 500px;
}
</style>
