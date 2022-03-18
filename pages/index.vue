<template>
  <!-- <Tutorial /> -->
  <px-login />
</template>

<script>
import PxLogin from '@/pages/login/index.vue'

export default {
  name: 'IndexPage',
  components: { PxLogin },
  layout(context) {
    return null
  },
}
</script>
