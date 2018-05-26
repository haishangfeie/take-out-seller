<template>
  <div id="app">
    <seller-header :seller="seller">
    </seller-header>
    <div class="nav">
      <router-link to="/goods">商品</router-link>
      <router-link to="/ratings">评价</router-link>
      <router-link to="/sellers">商家</router-link>
    </div>
    <router-view></router-view>
  </div>
</template>

<script>
import sellerHeader from './components/sellerHeader/sellerHeader'
import axios from 'axios'
const ERR_OK = 0
export default {
  components: {
    sellerHeader
  },
  data () {
    return {
      seller: {}
    }
  },
  created () {
    axios.get('api/seller')
      .then((res) => {
        const data = res.data
        if (!data.errno === ERR_OK) {
          return
        }
        this.seller = data.data
        console.log(this.seller)
      })
  },
  methods: {

  }
}
</script>

<style lang="stylus" scoped>

</style>
