<template>
  <div class="page-wrapper">
    <div class="container has-text-centered">
      <div v-if="beforeSent" class="column is-4 is-offset-4">
        <h3 class="title has-text-grey">Reset Password</h3>
        <h6 class="has-text-grey">Reset your password by providing your account email below.</h6>
        <div class="box">
          <form>
            <div class="field">
              <div class="control">
                <input
                  v-model="form.email"
                  class="input is-large"
                  type="email"
                  placeholder="Your Email"
                  autofocus=""
                  autocomplete="email">
                <form-errors :errors="v$.form.email.$errors" />
              </div>
            </div>
            <button
              @click="resetPassword"
              :disabled="isProcessing"
              type="button"
              class="button is-block is-info is-large is-fullwidth"
            >
              Next
            </button>
          </form>
        </div>
      </div>
      <div v-else class="column is-4 is-offset-4">
        <h3 class="title has-text-grey">Check your email</h3>
        <h6 class="has-text-grey">
            You'll receive a link in the email you supplied that will enable you to reset your account password.
        </h6>
        <p class="subtitle">{{form.email}}</p>
        <h6 class="has-text-grey">
            If you don't see the email, check other places it might be, like your junk, spam, social, or other folders.
        </h6>
        <button
            @click="backToResetSection"
            type="button"
            class="button is-block is-info is-large is-fullwidth"
        >
            Resend Email
        </button>
      </div>
    </div>
  </div>
</template>
<script>
import useAuth from '../composition/useAuth';
import useVuelidate from '@vuelidate/core'
import { required, email } from '@vuelidate/validators'
import FormErrors from "../components/FormErrors.vue";

export default {
  components: {
    FormErrors
  },
  data() {
    return {
      form: {
        email: "",
      },
      beforeSent: true,
    }
  },
  validations() {
    return {
      form: {
        email: { required, email },
      }
    }
  },
  setup() {
    return {
      ...useAuth(),
      v$: useVuelidate()
    };
  },
  watch: {
    isAuthenticated(isAuth) {
      if (isAuth) { this.$router.push("/"); }
    }
  },
  methods: {
    async resetPassword() {
      const isValid = await this.v$.$validate();
      const email = this.form.email;
      if (isValid) {
        this.$store.dispatch("user/resetPassword", this.form)
        .then(res => {
            console.log(res)
            this.$router.push({
                name: 'PasswordSent',
                params: { email }
            });
        });
      }
    },
  }
}
</script>

<style scoped>
  .hero.is-success {
    background: #F2F6FA;
  }
  .hero .nav, .hero.is-success .nav {
    -webkit-box-shadow: none;
    box-shadow: none;
  }
  .box {
    margin-top: 1rem;
  }
  .avatar {
    margin-top: -70px;
    padding-bottom: 20px;
  }
  .avatar img {
    padding: 5px;
    background: #fff;
    border-radius: 50%;
    -webkit-box-shadow: 0 2px 3px rgba(10,10,10,.1), 0 0 0 1px rgba(10,10,10,.1);
    box-shadow: 0 2px 3px rgba(10,10,10,.1), 0 0 0 1px rgba(10,10,10,.1);
  }
  input {
    font-weight: 300;
  }
  p {
    font-weight: 700;
  }
  p.subtitle {
    padding-top: 1rem;
  }
</style>
