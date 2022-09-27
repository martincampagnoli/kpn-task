<template>
  <div>
    <div class="container">
      <div class="row mb-4 mt-4">
        <div class="col-lg-3 col-sm-12 pl-0">
          <span>Has 5g? </span>
          <select v-model="has_5g" class="form-control" @change="applyFilter()">
            <option value="true">
              Yes
            </option>
            <option value="false">
              No
            </option>
          </select>
        </div>
        <div class="col-lg-3 col-sm-12 pl-0">
          <span>Filter by Name</span>
          <input v-model="name" type="text" class="form-control" placeholder="<enter name here>" @keyup="applyFilter()">
        </div>
        <div class="col-lg-3 col-sm-12 pl-0">
          <span>Filter by Color</span>
          <select v-model="color" class="form-control" @change="applyFilter()">
            <option v-for="c in colors" :key="c" :value="c">
              {{ c }}
            </option>
          </select>
        </div>
        <div class="col-lg-3 col-sm-12 pl-0 d-flex justify-content-center align-items-end">
          <button class="btn btn-primary" @click="clearFilters()">
            Clear Filters
          </button>
        </div>
      </div>
    </div>

    <div class="container">
      <div v-if="filteredPhones.length > 0" class="row">
        <div class="card-deck">
          <div v-for="item in filteredPhones" :key="item.id">
            <phone :phone="item" />
            <br>
          </div>
        </div>
      </div>
      <div v-if="filteredPhones.length === 0">
        There are no phones to display, try to update or remove filters
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Phone from './PhoneItem.vue'

export default {
  components: { Phone },
  data () {
    return {
      phones: {},
      filteredPhones: {},
      name: '',
      has_5g: '',
      color: '',
      colors: [
        'Blauw',
        'Goud',
        'Grafiet',
        'Zilver',
        'Zwart',
        'Grijs',
        'Wit',
        'Rood',
        'Geel',
        'Groen',
        'Paars',
        'Mint',
        'Creme',
        'Violet',
        'Dark Pearl',
        'Magic Blue',
        'Electric Graphite'
      ]
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
      this.filteredPhones = this.filterPhonesBy5g(this.filterPhonesByName(this.filterPhonesByColor(this.phones)))
    },
    filterPhonesBy5g (phones) {
      if (!this.has_5g) { return phones }
      return phones.filter(e => e.has_5g === JSON.parse(this.has_5g))
    },
    filterPhonesByName (phones) {
      if (!this.name) { return phones }
      return phones.filter(e => e.name.toLowerCase().includes(this.name.toLowerCase()))
    },
    filterPhonesByColor (phones) {
      if (!this.color) { return phones }
      return phones.filter(e => e.colors.includes(this.color.toUpperCase()))
    },
    clearFilters () {
      this.name = ''
      this.has_5g = undefined
      this.color = ''
      this.applyFilter()
    }
  }
}
</script>

<style>
</style>
