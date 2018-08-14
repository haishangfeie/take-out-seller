<template>
  <div class="shopcart-wrap">
    <div class="left">
      <div class="shopcart-icon-wrap">
        <span class="icon-shopping_cart"></span>
      </div>
      <div class="price">￥0</div>
      <div class="text">另需配送费￥4元</div>
    </div>
    <button class="btn">￥20起送</button>
  </div>
</template>

<script>
export default {}
</script>

<style scoped lang="stylus">
.shopcart-wrap
  position: fixed
  bottom: 0
  display: flex
  width: 100%
  height: 48px
  background: #141d27
  color: rgba(255, 255, 255, 0.4)
  .left
    flex: 1
    display: flex
    height: 48px
    .shopcart-icon-wrap
      margin-top: -10px
      margin-left: 12px
      flex: 0 0 56px
      width: 56px
      height: 56px
      border-radius: 50%
      background: #141d27
      overflow: hidden
      .icon-shopping_cart
        display: block
        width: 44px
        height: 44px
        border-radius: 50%
        background: #2b343c
        margin: 6px auto
        overflow: hidden
        font-size: 20px
        text-align: center
        line-height: 44px
    .price
      margin: 12px 12px 12px 0;
      padding: 0 12px
      height: 24px
      line-height: 24px
      font-size: 16px
      font-family: 'MicroSoft YaHei'
      font-weight: bold
      border-right: 1px solid #2c343d
    .text
      height 48px
      line-height 48px
      font-size:10px
  .btn
    flex: 0 0 105px
    width: 105px
    height: 48px
    line-height: 48px
    font-size: 12px
    font-weight: 700
    background: #2b333b
</style>
