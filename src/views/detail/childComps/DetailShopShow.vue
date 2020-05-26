<template>
  <div class="detail-shop-show">
    <div class="shop">
      <img :src="shop.logo ">
      <span class="name">{{ shop.name }}</span>
    </div>
    <div class="count">
      <div class="sells">
        <div>{{ shop.sells | sellCountFilter }}</div>
        <div>总销量</div>
      </div>
      <div class="goods-count">
        <div>{{ shop.goodsCount }}</div>
        <div>全部宝贝</div>
      </div>
      <div class="score">
        <table>
          <tr v-for="(item, index) in shop.score" :key="index">
            <td>{{ item.name }}</td>
            <td class="score-color" :class="{'score-better': item.isBetter}">{{ item.score }}</td>
            <td class="better-color" :class="{'better-more': item.isBetter}"><span>{{ item.isBetter ? '高':'低' }}</span></td>
          </tr>
        </table>
      </div>
    </div>
    <div class="button">
      <button>进店逛逛</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "DetailShopShow",
  props: {
    shop: {
      type: Object,
      default() {
        return {}
      }
    }
  },
  filters: {
    sellCountFilter: function (value) {
      if(value < 10000) return value
      return (value/10000).toFixed(1) + '万'
    }
  }
}
</script>

<style scoped>
.detail-shop-show {
  padding-bottom: 30px;
  box-shadow: 0 1px 1px rgba(100,100,100,.1);
}

.shop {
  position: relative;
  height: 60px;
  margin-bottom: 20px;
}

.shop img {
  width: 40px;
  height: 40px;
  border-radius: 20px;
  border-style: solid;
  border-color: grey;
  margin-left: 20px;
  margin-top: 10px;
}

.name {
  position: absolute;
  margin-left: 10px;
  margin-top: 20px;
}

.count {
  position: relative;
  height: 54.4px;
  margin-bottom: 20px;
}

.sells {
  font-size: 14px;
  text-align: center;
  position: absolute;
  margin-left: 10%;
}

.goods-count {
  font-size: 14px;
  text-align: center;
  position: absolute;
  margin-left: 30%;
  padding-right: 20px;
  border-right-style: solid;
}

.score {
  position: absolute;
  margin-left: 60%;
  font-size: 14px;
}

.score .score-color {
  color: #5ea732;
}

.score .score-better {
  color: #f13e3a;
}

.score .better-color span {
  background-color: #5ea732;
  color: #fff;
  text-align: center;
}

.score .better-more span {
  background-color: #f13e3a;
}

.button {
  text-align: center;
}

.button>button {
  background-color: #f13e3a;
  color: #fff;
  border: 0;
  padding-left: 10px;
  padding-right: 10px;
  border-radius: 10px;
}
</style>