<template>
  <div v-if="Object.keys(detailInfo).length !== 0" class="goods-show">
      <div class="desc">{{ detailInfo.desc }}</div>
      <div class="key">{{ detailInfo.detailImage[0].key }}</div>
      <div class="list">
        <img v-for="(item, index) in detailInfo.detailImage[0].list" :key="index" :src="item" @load="imgLoad">
      </div>
  </div>
</template>

<script>
export default {
  name: "DetailGoods",
  props: {
    detailInfo: {
      type: Object
    }
  },
  data() {
    return {
      counter: 0,
      imagesLength: 0
    }
  },
  methods: {
    imgLoad() {
      // 判断所有的图片都加载完了，那么进行一次回调就可以了
      if (++this.counter === this.imagesLength) {
        this.$emit('imgLoad')
      }
    }
  },
  watch: {
    detailInfo() {
      // 获取图片的个数
      this.imagesLength = this.detailInfo.detailImage[0].list.length
    }
  }
}
</script>

<style scoped>
.desc {
  padding-top: 20px;
  font-size: 12px;
  color: #f13e3a;
}

.key {
  padding-top: 20px;
  color: black;
}

.list img {
  width: 100%;
  height: 100%;
}
</style>