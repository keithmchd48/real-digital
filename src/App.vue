<template>
  <div id="app">
    <MainLayout>
      <RealDigitalForm action="https://httpbin.org/post"
                       method="POST" @submit="onSubmit">
        <RealDigitalTextfield ref="name" v-model="name" name="name" validation="[a-z]+" :isFormSubmitted="isFormSubmitted">
          Name
        </RealDigitalTextfield>
        <p v-show="isNameInvalid" class="help is-danger">Invalid Name input</p>

        <RealDigitalTextfield ref="phone" v-model="phone" name="phone" validation="[0-9]+" :isFormSubmitted="isFormSubmitted">
          Phone
        </RealDigitalTextfield>
        <p v-show="isPhoneInvalid" class="help is-danger">Invalid Phone input</p>

        <RealDigitalTextfield ref="subject" v-model="subject" name="subject" :isFormSubmitted="isFormSubmitted">
          Subject
        </RealDigitalTextfield>
        <p v-show="isSubjectInvalid" class="help is-danger">Invalid Subject input</p>

        <RealDigitalButton @submit="onSubmit">
          Send
        </RealDigitalButton>
      </RealDigitalForm>
      <section class="is-flex is-justify-content-center mt-3">
        {{httpsResponse}}
      </section>
    </MainLayout>
  </div>
</template>

<script>
import axios from "axios"
import MainLayout from "@/layouts/MainLayout";
import RealDigitalForm from "@/components/RealDigitalForm";
import RealDigitalTextfield from "@/components/RealDigitalTextfield";
import RealDigitalButton from "@/components/RealDigitalButton";

export default {
  name: 'App',
  components: {
    MainLayout, RealDigitalForm, RealDigitalTextfield, RealDigitalButton
  },
  data () {
    return {
      name: '',
      phone: '',
      subject: '',
      isFormSubmitted: false,
      httpsResponse: ''
    }
  },
  computed: {
    // is the "name" text field valid after user clicks on Send button
    isNameInvalid() {
      return this.isFormSubmitted && !this.$refs.name.isInputRegexValid
    },
    // is the "phone" text field valid after user clicks on Send button
    isPhoneInvalid() {
      return this.isFormSubmitted && !this.$refs.phone.isInputRegexValid
    },
    // is the "subject" text field valid after user clicks on Send button
    isSubjectInvalid() {
      return this.isFormSubmitted && !this.$refs.subject.isInputRegexValid
    }
  },
  methods: {
    async onSubmit(event) {
      this.isFormSubmitted = true
      // if any of the fields is has an invalid input value, do not execute the api
      if (this.isNameInvalid || this.isPhoneInvalid || this.isSubjectInvalid) return
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
        this.httpsResponse = resp.data.json
        setTimeout(() => {this.httpsResponse = ''}, 6000)
        // reset all values
        this.name = ''
        this.phone = ''
        this.subject = ''
        this.isFormSubmitted = false
      } catch (e) {
        console.log(e)
      }
    }
  }
}
</script>

<style>
@import "~bulma/css/bulma.css";
</style>
