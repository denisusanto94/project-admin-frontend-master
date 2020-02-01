<template>
  <section class="section">
    <div class="container">
      <div class="columns">
        <div class="column is-4 is-offset-4">
          <h2 class="title has-text-centered">Register!</h2>

          <!-- <Notification :massage="massage" v-if="massage"/> -->
 
          <div v-if="massage" class="notification is-danger">
            <table>
              <tr v-for="(item, index) in massage" :key="index">
                 {{ item }}
              </tr>
            </table>
          </div>

          <form method="post" @submit.prevent="register">
            <div class="field">
              <label class="label">Full Name</label>
              <div class="control">
                <input
                  type="text"
                  class="input"
                  name="name"
                  v-model="regis.name"
                  required
                >
              </div>
            </div>
            <div class="field">
              <label class="label">Username</label>
              <div class="control">
                <input
                  type="text"
                  class="input"
                  name="username"
                  v-model="regis.username"
                  required
                >
              </div>
            </div>
            <div class="field">
              <label class="label">Email</label>
              <div class="control">
                <input
                  type="email"
                  class="input"
                  name="email"
                  v-model="regis.email"
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
                  v-model="regis.password"
                  required
                >
              </div>
            </div>
            <div class="field">
              <label class="label">Confirm Password</label>
              <div class="control">
                <input
                  type="password"
                  class="input"
                  name="password_confirmation"
                  v-model="regis.password_confirmation"
                  required
                >
              </div>
            </div>
            <div class="control">
              <button type="submit" class="button is-dark is-fullwidth">Register</button>
            </div>
          </form>

          <div class="has-text-centered" style="margin-top: 20px">
            Already got an account? <nuxt-link to="/login">Login</nuxt-link>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import Notification from '~/components/Notification'

export default {
  components: {
    Notification,
  },

  data() {
    return {
      regis:[],
      massage: null,
      data:[],
      status:[]
    }
  },
  mounted(){
      this.regis = {
        name:'',
        username: '',
        email: '',
        password: '',
        password_confirmation: '',
        username: '',
        email: '',
        password: '',

      }

  },
  methods: {
    async register() {
      try {
        await this.$axios.post('users', this.regis)
        await this.$auth.loginWith('local', {
          data: this.regis,
        })

        this.$router.push('/')
      } catch (e) {
        this.massage = e.response.data.errors
      }
    }
  }
}
</script>