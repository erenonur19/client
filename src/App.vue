<template>
  <div id>
  <Navbar /> 
  
  <router-view />
  </div>
</template>
<script>
import Navbar from '@/components/Navbar.vue'
import { onMounted } from '@vue/runtime-core'

export default {
  components: {
    Navbar,
  },
  
}
</script>


<style lang="scss">


</style>
