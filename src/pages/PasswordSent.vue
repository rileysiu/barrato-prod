<template>
  <div class="page-wrapper">
    <div class="container has-text-centered">
      <div class="column is-4 is-offset-4">
        <h3 class="title has-text-grey">Check your email</h3>
        <h6 class="has-text-grey">
            You'll receive a link in the email you supplied that will enable you to reset your account password.
        </h6>
        <p class="subtitle">{{this.$route.params.email}}</p>
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
export default {
  data() {
    return {}
  },
  watch: {
    isAuthenticated(isAuth) {
      if (isAuth) { this.$router.push("/"); }
    }
  },
  methods: {
    backToResetSection(){
        this.$router.push("/forgetpassword");
    }
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
