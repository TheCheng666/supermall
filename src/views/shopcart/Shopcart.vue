<template>
  <div class="cart">
    <!-- 导航栏 -->
    <nav-bar class="nav-bar">
      <div slot="center">购物车({{ cartLength }})</div>
    </nav-bar>

    <!-- 商品列表 -->
    <cart-list/>
  </div>
</template>

<script>
import NavBar from 'components/common/navbar/NavBar'

import CartList from './childComps/CartList'

export default {
  name: "Shopcart",
  components: {
    NavBar,
    CartList
  },
  computed: {
    cartLength() {
      return this.$store.state.cartList.length
    }
  },
}
</script>

<style scoped>
.cart {
  height: 100vh;
}

.nav-bar {
  background-color: var(--color-high-text);
  color: #fff;
}
</style>
