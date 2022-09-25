/* eslint-disable vue/require-prop-types */
<template>
  <div>
    Here render one phone
    {{ phone.name }}
  </div>
</template>

<script>
export default {
  props: ['phone'],
  created () {
    console.dir(this.phone)
  }
}
</script>

<style>

</style>
