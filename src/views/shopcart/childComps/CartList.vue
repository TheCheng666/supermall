<template>
  <div class="cart-list">
    <scroll  class="content" ref="scroll">
      <cart-list-item v-for="(item, index) in $store.state.cartList" :key="index" :itemInfo="item" />
    </scroll>
  </div>
</template>

<script>
import CartListItem from './CartListItem'

import Scroll from 'components/common/scroll/Scroll'

export default {
  name: "CartList",
  components: {
    CartListItem,
    Scroll,
  },
  activated() {
    this.$refs.scroll.refresh()
  }
}
</script>

<style scoped>
.cart-list {
  height: calc(100% - 44px - 49px - 40px);
}

.content {
  height: 100%;
  overflow: hidden;
}
</style>