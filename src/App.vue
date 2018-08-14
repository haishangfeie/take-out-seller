<template>
  <div id="app">
    <seller-header :seller="seller">
    </seller-header>
    <div class="nav">
      <router-link class="nav-item" active-class="highlight" to="/goods">商品</router-link>
      <router-link class="nav-item" active-class="highlight" to="/ratings">评价</router-link>
      <router-link class="nav-item" active-class="highlight" to="/sellers">商家</router-link>
    </div>
    <router-view :goods="goods"></router-view>
    <shopcart></shopcart>
  </div>
</template>

<script>
import sellerHeader from './components/sellerHeader/sellerHeader'
import shopcart from 'components/shopcart/shopcart'
import axios from 'axios'
const ERR_OK = 0
export default {
  components: {
    sellerHeader,
    shopcart
  },
  data() {
    return {
      seller: {},
      goods: []
    }
  },
  created() {
    axios
      .get('api/seller')
      .then(res => {
        const data = res.data
        if (!data.errno === ERR_OK) {
          return
        }
        this.seller = data.data
      })
      .catch(err => {
        throw err
      })
    axios
      .get('api/goods')
      .then(res => {
        const data = res.data
        if (!data.errno === ERR_OK) {
          return
        }
        this.goods = data.data
      })
      .catch(err => {
        throw err
      })
  },
  methods: {}
}
</script>

<style lang="stylus" scoped>
@import './common/stylus/mixin.styl'
#app
  .nav
    display: flex
    bdb-1px(rgba(7, 17, 27, 0.1))
    .nav-item
      flex: 1
      height: 40px
      line-height: 40px
      text-align: center
      font-size: 14px
      color: rgb(77, 85, 93)
      &.highlight
        color: rgb(240, 20, 20)
</style>
