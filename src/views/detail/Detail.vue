<template>
  <div id="detail">
    <detail-nav-bar class="detail-nav" @titleClick="titleClick" ref="nav" />
    <scroll class="content" ref="scroll" :probe-type="3" @scroll="contentScroll">
      <detail-swiper :top-images="topImages" />
      <detail-base-show :goods="goods" />
      <detail-shop-show :shop="shop" />
      <detail-goods-show :detail-info="detailInfo" @imgLoad="imgLoad" />
      <detail-param-show ref="param" :param-info="paramInfo" />
      <detail-comment ref="comment" :comment-info="commentInfo" />
      <goods-list ref="recommend" :goods="recommends" />
    </scroll>
  </div>
</template>

<script>
import DetailNavBar from './childComps/DetailNavBar'
import DetailSwiper from './childComps/DetailSwiper'
import DetailBaseShow from './childComps/DetailBaseShow'
import DetailShopShow from './childComps/DetailShopShow'
import DetailGoodsShow from './childComps/DetailGoodsShow'
import DetailParamShow from './childComps/DetailParamShow'
import DetailComment from './childComps/DetailComment'

import Scroll from 'components/common/scroll/Scroll'
import GoodsList from 'components/content/goods/GoodsList'

import {getDetail, getRecommend, Goods, Shop, GoodsParam} from 'network/detail'
import {debounce} from 'common/utils'

export default {
  name: "Detail",
  components: {
    DetailNavBar,
    DetailSwiper,
    DetailBaseShow,
    DetailShopShow,
    DetailGoodsShow,
    DetailParamShow,
    DetailComment,
    Scroll,
    GoodsList
  },
  data() {
    return {
      iid: null,
      topImages: [],
      goods: {},
      shop: {},
      detailInfo: {},
      paramInfo: {},
      commentInfo: {},
      recommends: [],
      itemImageListener: null,
      themeTopYs: [],
      getThemeTopY: null,
      currentIndex: 0
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

      // 3.获取店铺信息
      this.shop = new Shop(data.shopInfo)

      // 4.获取商品详情信息
      this.detailInfo = data.detailInfo

      // 5.获取参数的信息
      this.paramInfo = new GoodsParam(data.itemParams.info, data.itemParams.rule)

      // 6.获取评论的信息
      if (data.rate.cRate !== 0) {
        this.commentInfo = data.rate.list[0]
      }
    })

    // 3.请求推荐数据
    getRecommend().then(res => {
      this.recommends = res.data.list
    })

    // 4.给getThemeTopY赋值
    this.getThemeTopY = debounce(() => {
      this.themeTopYs = []
      this.themeTopYs.push(0)
      this.themeTopYs.push(this.$refs.param.$el.offsetTop - 44)
      this.themeTopYs.push(this.$refs.comment.$el.offsetTop - 44)
      this.themeTopYs.push(this.$refs.recommend.$el.offsetTop -44)
    })
  },
  mounted() {
    const refresh = debounce(this.$refs.scroll.refresh)

    this.itemImageListener = () => {
      refresh()
    }

    this.$bus.$on('itemImageLoad', this.itemImageListener)
  },
  destroyed() {
    this.$bus.$off('itemImageLoad', this.itemImageListener)
  },
  methods: {
    imgLoad() {
      this.$refs.scroll.refresh()

      this.getThemeTopY()
    },
    titleClick(index) {
      this.$refs.scroll.scrollTo(0, -this.themeTopYs[index], 500)
    },
    contentScroll(position) {
      // 1.获取y值
      const positionY = -position.y

      // 2.positionY和主题中值进行对比
      let length = this.themeTopYs.length
      for(let i = 0; i < length; i++) {
        if(this.currentIndex !== i && ((i < length - 1 && positionY > this.themeTopYs[i] && positionY < this.themeTopYs[i+1]) || (i === length - 1 && positionY > this.themeTopYs[i]))) {
          this.currentIndex = i;
          this.$refs.nav.currentIndex = this.currentIndex
        }
      }
    }
  }
}
</script>

<style scoped>
#detail {
  position: relative;
  z-index: 9;
  background-color: #fff;
  height: 100vh;
}

.detail-nav {
  position: relative;
  z-index: 9;
  background-color: #fff;
}

.content {
  height: calc(100% - 44px);
}
</style>