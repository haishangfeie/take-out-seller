<template>
  <div class="stars">
    <div v-for="(star,index) in starArr" :key="index" class="star" :class="[`star_${size}`,star]"></div>
  </div>
</template>

<script>
export default {
  computed: {
    starArr() {
      let arr = []
      let score = Math.floor(this.score * 2) / 2
      while (score >= 1) {
        score--
        arr.push('on')
      }
      if (score === 0.5) {
        arr.push('half')
      }
      while (arr.length !== 5) {
        arr.push('off')
      }
      return arr
    }
  },
  props: {
    score: {
      type: Number,
      default: 0
    },
    size: {
      type: Number
    }
  }
}
</script>

<style lang="stylus" scoped>
@import '../../common/stylus/mixin.styl'
.stars
  display: inline-block
  font-size: 0
  .star
    display: inline-block
    margin-right: 20px
    &.star_24
      width: 10px
      height: 10px
      background-size: 10px 10px
      &.half
        bg-image('./star24_half')
      &.on
        bg-image('./star24_on')
      &.off
        bg-image('./star24_off')
    &.star_36
      width: 15px
      height: 15px
      background-size: 15px 15px
      &.half
        bg-image('./star36_half')
      &.on
        bg-image('./star36_on')
      &.off
        bg-image('./star36_off')
    &.star_48
      width: 20px
      height: 20px
      background-size: 20px 20px
      &.half
        bg-image('./star48_half')
      &.on
        bg-image('./star48_on')
      &.off
        bg-image('./star48_off')
    &:last-child
      margin-right: 0
</style>
