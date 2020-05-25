# supermall

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

### 一.FeatureView

- 独立组件封装FeatureView
  - div>a>img

### 二.TabControl

- 独立组件的封装
  - props>titles
  - div>根据titles v-for遍历div -> span{{title}}
  - css相关
  - 选中哪一个tab，哪一个tab的文字颜色变色，下面的border-bottom也变色
    - currentIndex

### 三.首页商品数据的请求

## 3.1 设计数据结构，用于保存数据

goods: {

pop: page/list

new: page/list

sell: page/list

}

## 3.2 发送数据请求

- 在home.js中封装getHomeGoods(type,page)
- 在home.vue中，又在methods中getHomeGoods(type)
- 调用getHomeGoods('pop')/getHomeGoods('new')/getHomeGoods('sell')
  - page:动态的获取对应的page
- 获取到数据：res
  - this.goods[type].list.push(...res.data.list)
  - this.goods[type].page += 1

### 四.对商品数据进行展示

## 4.1封装GoodsList.vue组件

- props: goods -> list[30]
- v-for goods -> GoodsListItem[30]
- GoodsListItem -> GoodsItem(数据)

## 4.2封装GoodsListItem.vue组件

- props: goodsItem
- goodsItem 取出数据，并且使用正确的div/span/img基本标签进行展示

### 五.对滚动进行重构: Better-Scroll

## 5.1在index.html中使用Better-Scroll

- const bscroll = new BScroll(el,{})
- 注意：wrapper -> content -> 很多内容
- 1.监听滚动
  - probeType: 0/1/2(手指滚动)/3(只要是滚动)
  - bscroll.on('scroll',(position) => {})
- 2.上拉加载
  - pullUpLoad: true
  - bscroll.on('pullingUp',() => {})
- 3.click: false
  - button可以监听点击
  - div不可以

## 5.2在Vue项目中使用Better-Scroll

### 六.回到顶部

## 6.1对BackTop.vue组件的封装

## 6.2如何监听组件的点击

- 直接监听back-top的点击，但是可以直接监听？
  - 不可以，必须添加修饰.native
- 回到顶部
  - scroll对象，scroll.scrollTo(x,y,time)
  - this.$refs.scroll.scrollTo(0,0,1000)

## 6.3BackTop组件的显示和隐藏

- isShowBackTop: false
- 监听滚动，拿到滚动的位置：
  - -position.y > 1000 -> isShowBackTop: true
  - isShowBackTop = -position.y > 1000