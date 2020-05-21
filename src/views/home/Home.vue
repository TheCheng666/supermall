<template>
  <div id="home">
    <nav-bar class="home-nav"><div slot="center">超级商城</div></nav-bar>
  </div>
</template>

<script>
import NavBar from 'components/common/navbar/NavBar'

export default {
  name: "Home",
  components: {
    NavBar
  }
}
</script>

<style>
.home-nav {
  background-color: red;
  color: #fff;
}
</style>
