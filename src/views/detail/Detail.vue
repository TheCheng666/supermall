<template>
  <div id="detail">
    <detail-nav-bar/>
    <detail-swiper :top-images="topImages" />
    <detail-base-show :goods="goods" />
  </div>
</template>

<script>
import DetailNavBar from './childComps/DetailNavBar'
import DetailSwiper from './childComps/DetailSwiper'
import DetailBaseShow from './childComps/DetailBaseShow'

import {getDetail, Goods} from 'network/detail'

export default {
  name: "Detail",
  components: {
    DetailNavBar,
    DetailSwiper,
    DetailBaseShow
  },
  data() {
    return {
      iid: null,
      topImages: [],
      goods: {}
    }
  },
  created() {
    // 1.保存传入的id
    this.iid = this.$route.params.iid

    // 2.根据id请求详情数据
    getDetail(this.iid).then(res => {
      // 1.获取顶部的图片轮播数据
      const data = res.result
      this.topImages =data.itemInfo.topImages

      // 2.获取商品信息
      this.goods = new Goods(data.itemInfo, data.columns, data.shopInfo.services)
    })
  }
}
</script>

<style scoped>

</style>