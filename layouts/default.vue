<template>
  <div>
    <nav
      class="navbar header has-shadow is-primary"
      role="navigation"
      aria-label="main navigation"
    >
      <div class="navbar-brand">
        <nuxt-link to="/"
          ><span style="color: #FFF; margin-right: 10px">Home</span></nuxt-link
        >
        <p v-if="isAuthenticated">Hi, {{ user.email }}</p>
        <div v-else>
          <nuxt-link to="/login"
            ><span style="color: #FFF; margin-right: 10px"
              >Login</span
            ></nuxt-link
          >
          <nuxt-link to="/signup"
            ><span style="color: #FFF; margin-right: 10px"
              >Signup</span
            ></nuxt-link
          >
        </div>
        <div class="navbar-burger">
          <span />
          <span />
          <span />
        </div>
      </div>
    </nav>

    <section class="main-content columns">
      <div class="container column is-10">
        <nuxt />
      </div>
    </section>
  </div>
</template>

<script>
import { mapState, mapGetters } from 'vuex'

export default {
  data() {
    return {
      items: [
        {
          title: 'Home',
          icon: 'home',
          to: { name: 'index' }
        },
        {
          title: 'Inspire',
          icon: 'lightbulb',
          to: { name: 'inspire' }
        }
      ]
    }
  },

  computed: {
    ...mapState(['user']),
    ...mapGetters(['isAuthenticated'])
  }
}
</script>
