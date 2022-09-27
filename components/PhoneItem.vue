/* eslint-disable vue/require-prop-types */
<template>
  <div>
    <div class="card">
      <img class="card-img-top" :src="`/phones${randomValue}.jpeg`" alt="Card image cap">
      <div class="card-body">
        <h5 class="card-title">
          {{ phone.name }}
        </h5>
        <p class="card-text">
          {{ phone.model }}
          <br>
        </p>
        <div>
          Has 5G?:
          <span :class="{ 'text-success': phone.has_5g, 'text-danger': !phone.has_5g }">
            {{ phone.has_5g ? 'Yes' : 'No' }}
          </span>
        </div>
        <div>
          Has eSim?:
          <span :class="{ 'text-success': phone.has_esim, 'text-danger': !phone.has_esim }">
            {{ phone.has_esim ? 'Yes' : 'No' }}
          </span>
        </div>
        <div>
          Has promotion?:
          <span :class="{ 'text-success': phone.has_promotion, 'text-danger': !phone.has_promotion }">
            {{ phone.has_promotion ? 'Yes' : 'No' }}
          </span>
        </div>
        <div>
          Has usp?:
          <span :class="{ 'text-success': phone.usp, 'text-danger': !phone.usp }">
            {{ phone.usp ? 'Yes' : 'No' }}
          </span>
        </div>
        <div>
          Colors available:
          <span v-for="(color, index) in phone.colors" :key="color">
            <span v-if="index !== 0">, </span>
            {{ color }}
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['phone'],
  computed: {
    randomValue () {
      const randomValue = Math.floor(Math.random() * (3))
      return randomValue
    }
  }
}

</script>

<style>
.card{
  width:350px
}
.card-img-top {
  width:348px;
  height: 200px
}
</style>
