<template>
  <div v-if="Object.keys(goods).length !== 0" class="detail-base-show">
    <div class="title">
      <span>{{ goods.title }}</span>
    </div>
    <div class="price">
      <span class="n-price">{{ goods.newPrice }}</span>
      <span class="o-price">{{ goods.oldPrice }}</span>
      <span class="discount">{{ goods.discountDesc }}</span>
    </div>
    <div class="columns">
      <span>{{ goods.columns[0] }}</span>
      <span>{{ goods.columns[1] }}</span>
      <span>{{ goods.services[goods.services.length-1].name }}</span>
    </div>
    <div class="services">
      <span v-for=" index in goods.services.length-1" :key="index">
        <img :src="goods.services[index-1].icon">
        <span>{{ goods.services[index-1].name }}</span>
      </span>
    </div>
  </div>  
</template>

<script>
export default {
  name: "DetailBaseShow",
  props: {
    goods: {
      type: Object,
      default() {
        return {}
      }
    }
  }
}
</script>

<style scoped>
.detail-base-show {
  padding-left: 2px;
  padding-right: 2px;
}

.title {
  font-size: 16px;
  color: black;
  margin-bottom: 15px;
}

.price {
  margin-bottom: 20px;
}

.n-price {
  color: var(--color-high-text);
  font-size: 28px;
  margin-right: 10px;
}

.o-price {
  font-size: 14px;
  text-decoration: line-through;
  margin-right: 10px;
}

.discount {
  color: #fff;
  background-color: red;
  border-radius: 10px;
}

.columns {
  display: flex;
  padding-bottom: 10px;
  box-shadow: 0 1px 1px rgba(100,100,100,.1);
}

.columns>span{
  font-size: 12px;
  flex: 1;
  text-align: center;
}

.services {
  margin-top: 20px;
  display: flex;
  margin-bottom: 100px;
}

.services>span {
  font-size: 12px;
  flex: 1;
  text-align: center;
}

.services img {
  width: 12px;
  height: 12px;
}
</style>