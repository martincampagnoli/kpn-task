<template>
  <div>
    <div class="container">
      <div class="row">
        <div class="col-4">
          <span>Has 5g?</span>
          <select v-model="has_5g" class="form-control" @change="applyFilter()">
            <option value="">
              All
            </option>
            <option value="true">
              Yes
            </option>
            <option value="false">
              No
            </option>
          </select>
        </div>
        <div class="col-4">
          <span>Filter by Name</span>
          <input v-model="name" type="text" placeholder="Enter name here" @keyup="applyFilter()">
        </div>
        <div class="col-4">
          <span>Filter by Color</span>
          <input v-model="color" type="text" placeholder="Enter color here" @keyup="applyFilter()">
        </div>
      </div>
    </div>

    <div class="container">
      <div class="row">
        <div class="card-deck">
          <div v-for="item in filteredPhones" :key="item.id">
            <phone :phone="item" />
            <br>
          </div>
        </div>
      </div>
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
      phones: {},
      filteredPhones: {},
      name: '',
      has_5g: '',
      color: ''
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
          this.filteredPhones = this.phones
        })
    },
    applyFilter () {
      console.dir(this.filteredPhones)
      this.filteredPhones = this.filterPhonesBy5g(this.filterPhonesByName(this.filterPhonesByColor(this.phones)))
    },
    filterPhonesBy5g (phones) {
      if (!this.has_5g) { return phones }
      return phones.filter(e => e.has_5g === JSON.parse(this.has_5g))
    },

    filterPhonesByName (phones) {
      if (!this.name) { return phones }
      return phones.filter(e => e.name.toLowerCase().includes(this.name))
    },

    filterPhonesByColor (phones) {
      if (!this.color) { return phones }
      return phones.filter(e => e.colors.includes(this.color))
    }

  }

}
</script>

<style>

</style>
