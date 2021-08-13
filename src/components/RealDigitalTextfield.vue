<template>
  <div class="field">
    <label class="label">
      <slot></slot>
    </label>
    <div class="control">
      <input class="input" type="text"
             v-bind="$attrs"
             :class="[{'is-danger': !isInputRegexValid}]"
             :value="value"
             @input="onInputEvent">
      <p v-show="!isInputRegexValid" class="help is-danger">Invalid Name input</p>
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
    }
  },
  computed: {
    // if input value matches regex, return true. Else false
    isInputRegexValid() {
      if (!this.validation) return true
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
