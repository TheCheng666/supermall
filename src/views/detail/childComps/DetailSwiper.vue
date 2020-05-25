<template>
  <swiper class="detail-item">
    <swiper-item v-for="(item, index) in topImages" :key="index">
      <img :src="item">
    </swiper-item>
  </swiper>
</template>

<script>
import {Swiper, SwiperItem} from 'components/common/swiper'

export default {
  name: "DetailSwiper",
  components: {
    Swiper,
    SwiperItem
  },
  props: {
    topImages: {
      type: Array,
      default() {
        return []
      }
    }
  }
}
</script>

<style scoped>
.detail-item {
  height: 300px;
  overflow: hidden;
}

.detail-item img {
  height: 100%;
}
</style>