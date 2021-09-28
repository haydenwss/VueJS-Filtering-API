<template>
  <div class="splashscreen--wrapper">

    <!-- Starting state for leave. Added immediately when a leaving transition is triggered, removed after one frame -->
    <!-- *---------------------------------------------------------------------* -->
    <transition @leave="leaveScreen" v-on:after-appear="leaveScreen" appear>
      <div class="logo--wrapper"></div>
    </transition>
    <!-- LOOPING THROUGH logoName TEXT  -->

    <!-- *----------------------------* -->
    <div class="logo--letters--group">
      <span class="logo--letter" v-for="(item, index) in logoName" :key="index" >
        {{item}}
      </span>
    </div>
    <!-- *----------------------------* -->
  </div>
</template>
<script>
export default {
  name: 'SplashScreen',
  data () {
    return {
      show: true,
      logoName: ['.','.','.', ' ', 'THE', '  ', 'WIZARDING', '  ', 'WORLD', '  ', 'AWAITS', ' ', '.','.','.'],
    }
  },
  methods: {
    leaveScreen (el) {
      // once the animation is complete => redirects to '/home'
      this.$router.push('/home')
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../style/SplashScreen.scss'
</style>

