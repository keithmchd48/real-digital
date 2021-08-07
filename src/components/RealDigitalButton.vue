<template>
  <div class="field is-grouped">
    <div class="control">
      <button type="submit" @submit.prevent="emitSubmitEvent" class="button is-link">
        <slot></slot>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "RealDigitalButton",
  methods: {
    emitSubmitEvent(event) {
      this.$emit('submit', event)
    }
  }
}
</script>

<style scoped>

</style>
