<template>
  <div id="app">
    <MainLayout>
      <RealDigitalForm action="https://httpbin.org/post" ref="myForm"
                       method="POST" @form-submitted="formSubmitted">
        <RealDigitalTextfield ref="name" v-model="name" name="name" validation="[a-z]+">
          Name
        </RealDigitalTextfield>


        <RealDigitalTextfield ref="phone" v-model="phone" name="phone" validation="[0-9]+">
          Phone
        </RealDigitalTextfield>

        <RealDigitalTextfield ref="subject" v-model="subject" name="subject">
          Subject
        </RealDigitalTextfield>

        <RealDigitalButton>
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
      httpsResponse: '',
      timeout: null
    }
  },
  methods: {
    formSubmitted(payload) {
      this.httpsResponse = payload
      clearTimeout(this.timeout)
      this.timeout = setTimeout(() => {this.httpsResponse = ''}, 6000)
      // reset all values
      this.name = ''
      this.phone = ''
      this.subject = ''
    }
  }
}
</script>

<style>
@import "~bulma/css/bulma.css";
</style>
