/* eslint-disable vue/require-prop-types */
<template>
  <div>
    <div class="card" style="width:350px">
      <img class="card-img-top" :src="`https://source.unsplash.com/random/300x100?sig=${phone.id}`" alt="Card image cap">
      <div class="card-body">
        <h5 class="card-title">
          {{ phone.name }}
        </h5>
        <p class="card-text">
          {{ phone.model }}
          <br>
          <br>
          <span>has_5g: {{ phone.has_5g ? 'yes' : 'no' }}</span><br>
          <span>has_esim: {{ phone.has_esim ? 'yes' : 'no' }}</span><br>
          <span>has_promotion: {{ phone.has_promotion ? 'yes' : 'no' }}</span><br>
          <span>has_usp: {{ phone.has_usp ? 'yes' : 'no' }}</span><br>
          Colors available: <span v-for="color in phone.colors" :key="color">
            {{ color }} <br>
          </span>
        </p>
        <small class="text-muted"> -> See details</small>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['phone']
}
</script>

<style>
</style>
