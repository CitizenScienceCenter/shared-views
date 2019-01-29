<i18n>
  {
    "de": {
      "heading": "Anmelden"
    },
    "en": {
      "heading": "EN: Fragen und Antworten"
    }
  }
</i18n>

<template>
  <div>
    <app-content-section>
      <div class="content-wrapper">

        <div class="row row-centered row-centered">

          <div class="col col-large-5 col-wrapping col-large-no-bottom-margin">

              <h2 class="heading">Login</h2>
              <login-form></login-form>

          </div>

          <div class="col col-large-5 col-wrapping col-no-bottom-margin">

              <h2 class="heading">Create an Account</h2>
              <register-form></register-form>

          </div>

        </div>

      </div>
    </app-content-section>

    <app-footer></app-footer>

  </div>
</template>

<script>
  import LoginForm from '@/components/shared/LoginForm.vue'
  import RegisterForm from '@/components/shared/RegisterForm.vue'
  import ContentSection from '@/components/shared/ContentSection.vue'
  import Footer from '@/components/shared/Footer.vue'

  export default {
  name: "Login",
  components :{
    LoginForm,
      RegisterForm,
      'app-content-section': ContentSection,
      'app-footer': Footer
  }
};
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
