<template>
  <div>
    <div class="colums">
      <div class="column">
        <img :src="item.img" style="height: 400px" />
      </div>
      <div class="column">
        <p>{{ item.name }}</p>
        <p>{{ item.description }}</p>
        <p>{{ item.price }}</p>
        <p>{{ item.inventory }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import fb from '~/plugins/firebase'

export default {
  data() {
    return {
      item: {
        name: 'Summer Flower Print Shirt',
        description: "It's so cute!",
        price: '¥5980(+tax)',
        inventory: 10,
        img: ''
      }
    }
  },

  mounted() {
    const that = this
    const storage = fb.storage()
    const ref = storage.ref('images/first-view-01.jpg')
    ref.getDownloadURL().then(function(url) {
      that.item.img = url
    })
  }
}
</script>
