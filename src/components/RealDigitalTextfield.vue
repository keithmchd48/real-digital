<template>
  <div class="field">
    <label class="label">
      <slot></slot>
    </label>
    <div class="control">
      <input class="input" type="text"
             v-bind="$attrs"
             :class="[{'is-danger': isFormSubmitted && !isInputRegexValid}]"
             :value="value"
             @input="onInputEvent">
    </div>
  </div>
</template>

<script>
export default {
  name: "RealDigitalTextfield",
  inheritAttrs: false,
  props: {
    validation: {
      type: String,
      required: false
    },
    value: {
      type: String,
      value: "",
    },
    isFormSubmitted: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    // if input value matches regex, return true. Else false
    isInputRegexValid() {
      const regex = new RegExp(this.validation, 'g')
      return regex.test(this.value)
    }
  },
  methods: {
    onInputEvent(event) {
      this.$emit("input", event.target.value);
    },
  }
}
</script>

<style scoped>

</style>
