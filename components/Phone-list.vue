<template>
  <div>
    <span>Here render phone list</span>
    <div v-for="item in phones" :key="item.id">
      <phone :phone="item" />
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Phone from './Phone.vue'

export default {
  components: { Phone },
  data () {
    return {
      phones: {}
    }
  },
  mounted () {
    this.getPhones()
  },
  methods: {
    getPhones () {
      axios.get('/phone_feed.json')
        .then((response) => {
          this.phones = response.data.products
        })
    }
  }

}
</script>

<style>

</style>
