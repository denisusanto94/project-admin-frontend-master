<template>
  <section class="section">
    <div class="container">
      <div class="columns">
        <div class="column is-4 is-offset-4">
          <h2 class="title has-text-centered">Welcome back!</h2>

           <!-- <Notification :massage="massage" v-if="massage"/> -->

          <div v-if="massage" class="notification is-danger">
            <p>
              Username / Password Salah
            </p>
          </div>

          <form method="post" @submit.prevent="login">
            <div class="field">
              <label class="label">Email</label>
              <div class="control">
                <input
                  type="email"
                  class="input"
                  name="email"
                  v-model="loginForm.email"
                  required
                >
              </div>
            </div>
            <div class="field">
              <label class="label">Password</label>
              <div class="control">
                <input
                  type="password"
                  class="input"
                  name="password"
                  v-model="loginForm.password"
                  required
                >
              </div>
            </div>
            <div class="control">
              <button type="submit" class="button is-dark is-fullwidth">Log In</button>
            </div>
          </form>
          <div class="has-text-centered" style="margin-top: 20px">
            <p>
              Don't have an account? <nuxt-link to="/register">Register</nuxt-link>
            </p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import Notification from '~/components/Notification'

export default {
  middleware: 'guest',
  components: {
    Notification,
  },

  data() {
    return {
      loginForm:[],
      token:null,
      error: null,
      massage: null
    }
  },
  mounted(){
    this.loginForm = {
      email: '',
      password: '',
    }
  },

  methods: {
    async login() {
      // console.log(this.loginForm)
      try {
        await this.$auth.loginWith('local', {
          data: this.loginForm
        })

        this.$router.push('/')
      } catch (e) {
        this.massage = e.response.data.error
      }
    }
  }
}
</script>