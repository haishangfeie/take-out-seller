<template>
  <div class="headline">
    <div class="line"></div>
    <div class="title">{{title}}</div>
    <div class="line"></div>
  </div>
</template>

<script>
export default {
  props: {
    title: {
      type: String
    }
  }
}
</script>

<style lang="stylus" scoped>
.headline
  width: 100%
  margin: 28px auto 24px
  display:flex
  .line
    flex:1
    &:before
      display block
      content:' '
      width 100%
      height 1px
      margin-top 7px
      background rgba(255,255,255,.2)
  .title
    padding 0 12px
    line-height 14px
    font-size 14px
    font-weight 700
    color:#fff
</style>
