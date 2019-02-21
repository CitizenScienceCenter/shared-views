<i18n>
  {

  "en": {

  "page-title": "Reset Password",

  "heading": "Reset Password",
  "label-email": "Email",
  "button-reset": "Reset"

  },

  "de": {

  "page-title": "Passwort zurücksetzen",

  "heading": "Passwort zurücksetzen",
  "label-email": "Email",
  "button-reset": "Zurücksetzen"

  }

  }
</i18n>


<template>
  <div>
    <app-content-section>
      <div class="content-wrapper">

          <div class="row row-centered">
            <div class="col col-large-6">

              <h2 class="heading">{{ $t('heading') }}</h2>
              <form>
                <div class="form-field form-field-block">
                  <label for="email">{{ $t("label-email") }}</label>
                  <input v-model="email" type="email" name="email" id="email" autocomplete="email" :disabled="loading" />
                </div>
                <div class="button-group right-aligned">
                  <button @click.prevent="request" type="submit" class="button button-primary" :disabled="loading">{{ $t('button-reset') }}</button>
                </div>
            </form>
            <p v-if="success" class="success">Bitte überprüfe deine E-Mails</p>

            </div>
          </div>

      </div>
    </app-content-section>

    <app-footer></app-footer>

  </div>
</template>

<script>
import { mapState, mapGetters } from "vuex";
import ContentSection from '@/components/shared/ContentSection.vue'
import Footer from '@/components/shared/Footer.vue'

export default {
  name: "RequestReset",
  components :{
      'app-content-section': ContentSection,
      'app-footer': Footer
  },
  data() {
    return {
      email: undefined,
      success: false
    }
  },
  computed: mapState({
    loading: state => state.settings.loading
  }),
    metaInfo: function() {
        return {
            title: this.$t('page-title')
        }
    },
  mounted() {
  },
  methods: {

    request() {
        console.log('dispatch request');
      this.$store.dispatch('c3s/user/requestReset', this.email ).then(res => {
          console.log('request came back');
        console.log(res);
        if (res) {
          this.success = true
        }
      });

    }

  }
};
</script>

