<template>
  <form @submit.prevent="onSubmit">
    <slot></slot>
  </form>
</template>

<script>
import axios from "axios";

export default {
  name: "RealDigitalForm",
  data () {
    return {
      isFormSubmitted: false,
    }
  },
  computed: {
    areFieldsValid () {
      let valid = true
      this.$slots.default.forEach((item) => {
        if (item.tag === 'vue-component-2-RealDigitalTextfield' && !item.child.isInputRegexValid) valid = false
      })
      return valid
    },
  },
  methods: {
    async onSubmit(event) {
      this.isFormSubmitted = true
      if (!this.areFieldsValid) return
      try {
        // extract the form action and method attribute values
        const { action, method } = event.target
        // extract the form input values
        const { name, phone, subject } = Object.fromEntries(new FormData(event.target))
        // "method" can be "get", "post", "put", etc
        // action is the api url to be hit
        const resp = await axios[method](action, {
          name, phone, subject
        })
        this.$emit('form-submitted', resp.data.json)
        this.isFormSubmitted = false
      } catch (e) {
        console.log(e)
      }
    }
  }
}
</script>

<style scoped>

</style>
