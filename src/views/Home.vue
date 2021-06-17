<template>
  <div class="home">
    <Header></Header>
  </div>
</template>

<script>
import Header from '@/components/Header.vue'
export default {
  name: 'Home',
  components: {
    Header
  }
}
</script>
<style lang="scss" scoped>
.home {
  margin: 0 auto;
  max-width: 350px;
}
</style>
