<template>
  <div class="header">
    <div class="header-left">
      <img class="avatar" :src="seller.avatar" alt="" width="64" height="64">
    </div>
    <div class="header-right">
      <div class="title-warp">
        <span class="brand"></span>
        <h1 class="title">{{seller.name}}</h1>
      </div>
      <div class="desc">
        {{seller.description}}/{{seller.deliveryTime}}分钟送达
      </div>
      <div class="supports" v-if="seller.supports">
        <i class="tag" :class="mapClass(seller.supports[0].type)"></i>
        <span class="description">{{seller.supports[0].description}}</span>
      </div>
    </div>
    <div class="bulletin">
      <i class="bulletin-img"></i>
      <div class="text">{{seller.bulletin}}</div>
      <span class="icon-keyboard_arrow_right"></span>
    </div>
    <div class="count-wrap" @click="showDetail" v-if="seller.supports">
      <span class="count">{{seller.supports.length}}个</span>
      <span class="icon-keyboard_arrow_right"></span>
    </div>
    <div class="bg">
      <img :src="seller.avatar" width="100%" height="100%" alt="">
    </div>
    <div class="mask" v-if="isShowDetail"></div>
    <div class="mask-content" v-if="isShowDetail" ref="maskContent">
      <div style="min-height:100%;">
        <div class="content-wrap">
          <div class="content">
            <div class="name">{{seller.name}}</div>
            <div class="star-warp">
              <star :size=48 :score="seller.score"></star>
            </div>
            <headline title="优惠信息"></headline>
            <ul class="supports">
              <li class="support-item" v-for="(support,index) in seller.supports" :key="index">
                <i class="tag" :class="mapClass(support.type)"></i>
                <div class="text">{{support.description}}</div>
              </li>
            </ul>
            <headline title="商家公告"></headline>
            <div class="bulletin-text">
              {{seller.bulletin}}
            </div>
          </div>
        </div>
        <div class="close">
          <span class="icon-close"></span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import star from '../star/star'
import headline from '../headline/headline'
import BScroll from 'better-scroll'
export default {
  watch: {
    isShowDetail(val) {
      if (val) {
        this.$nextTick(() => {
          this._initBScroll()
        })
      }
    }
  },
  components: {
    star,
    headline
  },
  methods: {
    _initBScroll() {
      if (!this.maskContent) {
        this.maskContent = new BScroll(this.$refs.maskContent, {})
      } else {
        this.maskContent.refresh()
      }
    },
    mapClass(index) {
      return this.classMap[index]
    },
    showDetail() {
      this.isShowDetail = true
    }
  },
  data() {
    return {
      maskContent: null,
      isShowDetail: false,
      classMap: ['decrease', 'discount', 'special', 'invoice', 'guarantee']
    }
  },
  props: {
    seller: {
      type: Object,
      default() {
        return {}
      }
    }
  }
}
</script>

<style lang="stylus" scoped>
@import '../../common/stylus/mixin.styl'
.header
  position: relative
  display: flex
  box-sizing: border-box
  width: 100%
  height: 134px
  padding: 24px 0 0 24px
  background: rgba(7, 17, 27, 0.5)
  .header-left
    flex: 0 0 64px
    width: 64px
    height: 64px
    margin-right: 16px
    .avatar
      border-radius: 2px
  .header-right
    flex: 1
    .title-warp
      font-size: 0
      .brand, .title
        display: inline-block
        vertical-align: top
      .brand
        width: 30px
        height: 18px
        background-size: 30px 18px
        bg-image('brand')
        border-radius: 2px
      .title
        margin-left: 6px
        margin-bottom: 8px
        line-height: 18px
        font-size: 16px
        font-weight: bold
        color: #fff
    .desc
      margin-bottom: 10px
      line-height: 12px
      font-size: 12px
      color: #fff
    .supports
      font-size: 0
      .tag
        display: inline-block
        margin-right: 4px
        width: 12px
        height: 12px
        background-size: 12px 12px
        border-radius: 2px
        &.decrease
          bg-image('decrease_1')
        &.discount
          bg-image('discount_1')
        &.special
          bg-image('special_1')
        &.invoice
          bg-image('invoice_1')
        &.guarantee
          bg-image('guarantee_1')
      .description
        vertical-align: top
        line-height: 12px
        font-size: 10px
        color: #fff
  .bulletin
    position: absolute
    left: 0
    bottom: 0
    display: flex
    width: 100%
    height: 28px
    background: rgba(7, 17, 27, 0.2)
    color: #fff
    .bulletin-img
      flex: 0 0 22px
      width: 22px
      height: 12px
      margin: 8px 4px 0 12px
      background-size: 22px 12px
      bg-image('bulletin')
    .text
      display: inline-block
      margin-right: 20px
      flex: 1
      line-height: 28px
      vertical-align: middle
      height: 28px
      font-size: 10px
      // 超出字隐藏
      overflow: hidden
      white-space: nowrap
      text-overflow: ellipsis
    .icon-keyboard_arrow_right
      position: absolute
      top: 8px
      right: 12px
      font-size: 10px
      font-weight: 200
  .count-wrap
    position: absolute
    right: 12px
    bottom: 43px
    height: 24px
    padding: 0 8px
    background: rgba(0, 0, 0, 0.2)
    border-radius: 24px
    font-size: 0
    color: #fff
    .count
      vertical-align: top
      line-height: 24px
      font-size: 10px
    .icon-keyboard_arrow_right
      vertical-align: top
      line-height: 24px
      font-size: 10px
  .bg
    position: absolute
    top: 0
    bottom: 0
    left: 0
    right: 0
    z-index: -1
    filter: blur(10px)
  .mask
    position: fixed
    top: 0
    bottom: 0
    left: 0
    right: 0
    z-index: 100
    background: rgba(7, 17, 27, 0.8)
  .mask-content
    position: fixed
    left: 0
    top: 0
    width: 100%
    height: 100%
    z-index: 101
    overflow: hidden
    .content-wrap
      width: 80%
      min-height: 100%
      margin: 0 auto
      .content
        padding: 64px 0
        color: #fff
        font-size: 0
        .name
          line-height: 16px
          text-align: center
          font-size: 16px
          font-weight: 700
          color: #fff
        .star-warp
          margin: 16px 0 28px
          text-align: center
        .supports
          .support-item
            margin: 0 0 12px 12px
            .tag
              display: inline-block
              margin-right: 4px
              width: 16px
              height: 16px
              background-size: 16px 16px
              border-radius: 2px
              &.decrease
                bg-image('decrease_2')
              &.discount
                bg-image('discount_2')
              &.special
                bg-image('special_2')
              &.invoice
                bg-image('invoice_2')
              &.guarantee
                bg-image('guarantee_2')
            .text
              vertical-align: top
              display: inline-block
              margin-left: 6px
              line-height: 16px
              font-size: 12px
              color: #fff
        .bulletin-text
          padding: 0 12px
          line-height: 24px
          font-size: 12px
    .close
      position: relative
      margin-top: -64px
      text-align: center
      .icon-close
        font-size: 32px
        color: rgba(255, 255, 255, 0.5)
</style>
