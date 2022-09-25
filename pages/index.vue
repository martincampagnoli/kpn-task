<template>
  <phone-list />
</template>

<script lang="ts">
import Vue from 'vue'
import PhoneList from '~/components/Phone-list.vue'

export default Vue.extend({
  name: 'IndexPage',
  components: { PhoneList }
})
</script>
