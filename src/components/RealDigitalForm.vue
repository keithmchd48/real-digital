<template>
  <form @submit.prevent="emitSubmitEvent">
    <slot></slot>
  </form>
</template>

<script>
export default {
  name: "RealDigitalForm",
  methods: {
    emitSubmitEvent(event) {
      this.$emit('submit', event)
    }
  }
}
</script>

<style scoped>

</style>
