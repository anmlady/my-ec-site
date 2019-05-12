<template>
  <div>
    <slot></slot>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  computed: {
    ...mapGetters(['isAuthenticated'])
  },

  mounted() {
    if (!this.isAuthenticated) {
      this.$router.push('/login')
    }
  }
}
</script>
