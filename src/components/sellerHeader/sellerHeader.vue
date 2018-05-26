<template>
  <div class="header">
    <div class="header-left">
      <img class="avatar" :src="seller.avatar" alt="" width="64" height="64">
    </div>
    <div class="header-right">
      <div class="title-warp">
        <span class="brand"></span><h1 class="title">{{seller.name}}</h1>
      </div>
      <div class="desc">
        {{seller.description}}/{{seller.deliveryTime}}分钟送达
      </div>
      <div class="supports" v-if="seller.supports">
        <i></i>{{seller.supports[0].description}}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    seller: {
      type: Object,
      default () {
        return {}
      }
    }
  }
}
</script>

<style lang="stylus" scoped>
  @import "../../common/stylus/mixin.styl";
  .header
    display:flex
    box-sizing:border-box
    width :100%
    height :134px
    padding:24px 0 0 24px
    background #ccc
    .header-left
      flex: 0 0 64px
      width:64px
      height:64px
      margin-right:16px
      .avatar
        border-radius:2px
    .header-right
      flex:1
      .title-warp
        font-size:0
        .brand,.title
          display inline-block
          vertical-align:top
        .brand
          width 30px
          height 18px
          background-size:30px 18px
          bg-image('brand')
          border-radius:2px
        .title
          margin-left 6px
          margin-bottom 8px
          line-height 18px
          font-size:16px
          font-weight:bold
          color:#fff
        .desc
          margin-bottom 10px
          line-height 12px
          font-size:12px
          color:#fff
</style>
