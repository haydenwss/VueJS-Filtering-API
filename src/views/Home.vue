<template>
  <div class="home">
    <SearchBarInput />
    <!-- <Results /> -->
  </div>
</template>

<script>
// @ is an alias to /src
import SearchBarInput from '@/components/SearchBarInput.vue'
// import Results from '@/components/Results.vue'

export default {
  name: 'Home',
  components: {
    SearchBarInput,
    // Results
  }
}
</script>

<style lang="scss" scoped>
@import '../style/HomeStyle.scss'
</style>