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
      <button class="button is-primary" @click="login">
        Login
      </button>
    </div>
  </div>
</template>

<script>
import firebase from '~/plugins/firebase'
import { mapActions, mapState, mapGetters } from 'vuex'

export default {
  data() {
    return {
      email: null,
      password: null,
      errorMessage: null
    }
  },

  mounted() {
    firebase.auth().onAuthStateChanged(user => {
      this.setUser(user)
    })
  },

  computed: {
    ...mapState(['user']),
    ...mapGetters(['isAuthenticated'])
  },

  methods: {
    ...mapActions(['setUser']),
    login() {
      firebase
        .auth()
        .signInWithEmailAndPassword(this.email, this.password)
        .then(user => {
          alert('logged in!')
          this.$router.push('/')
        })
        .catch(error => {
          this.errorMessage = 'Error: ' + error + 'Please try again'
        })
    },
    logout() {
      firebase
        .auth()
        .signOut()
        .then(() => {
          this.setUser(null)
        })
        .catch(error => {
          this.errorMessage = 'Error: ' + error + 'Please try again'
        })
    }
  }
}
</script>
