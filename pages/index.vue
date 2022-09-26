<template>
  <div>
    <PhoneList />
    <FooterElement />
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import FooterElement from '~/components/FooterElement.vue'
import PhoneList from '~/components/PhoneList.vue'

export default Vue.extend({
  name: 'IndexPage',
  components: { PhoneList, FooterElement }
})
</script>
