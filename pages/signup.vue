<template>
  <div>
    <div v-if="isAuthenticated">
      <p>Logged in as {{ user.email }}!</p>
      <p><a @click="logout">Logout</a></p>
    </div>
    <div v-else>
      <b-field label="User ID">
        <b-input v-model="email"></b-input>
      </b-field>
      <b-field label="PassWord">
        <b-input v-model="password"></b-input>
      </b-field>
      <button class="button is-primary" @click="signup">
        Signup
      </button>
    </div>
  </div>
</template>

<script>
import fb from '~/plugins/firebase'

export default {
  data() {
    return {
      email: null,
      password: null,
      errorMessage: null
    }
  },

  methods: {
    signup() {
      fb.auth()
        .createUserWithEmailAndPassword(this.email, this.password)
        .then(user => {
          this.$router.push('/')
        })
        .catch(error => {
          if (error) {
            this.errorMessage = error
            alert(error)
          }
        })
    }
  }
}
</script>
