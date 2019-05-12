<template>
  <div>
    <div class="columns">
      <div v-for="img in images" :key="img" class="column">
        <nuxt-link to="/item">
          <img :src="img" />
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
import fb from '~/plugins/firebase'

export default {
  data() {
    return {
      images: []
    }
  },

  mounted() {
    const that = this
    const storage = fb.storage()
    const ref = storage.ref('images/first-view-01.jpg')
    ref.getDownloadURL().then(function(url) {
      for (let i = 0; i < 3; i++) {
        that.images.push(url)
      }
    })
  }
}
</script>

<style>
img {
  height: 400px;
}
</style>
