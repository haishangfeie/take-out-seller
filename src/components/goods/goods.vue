<template>
  <div>
    <div class="goods-wrap">
      <div class="goods">
        <div class="goods-left" ref="goodsLeft">
          <ul class="list">
            <li v-for="(item,index) in goods" :key="index" class="item" :class="{highlight:index===nowIndex}" ref="leftItem" @click="selFoodsItem(index,$event)">
              <div class="content">
                <i v-show="item.type!==-1" class="tag" :class="mapClass(item.type)"></i>
                <span class="text">{{item.name}}</span>
              </div>
            </li>
          </ul>
        </div>
        <div class="goods-right" ref="goodsRight">
          <ul class="list">
            <li class="item" v-for="(item,item_index) in goods" :key="item_index" ref="listItem">
              <div class="title">{{item.name}}</div>
              <ul class="good-list">
                <li class="good" v-for="(good,good_index) in item.foods" :key="good_index">
                  <img class="icon" :src="good.icon" alt="">
                  <div class="content">
                    <div class="name">{{good.name}}</div>
                    <div class="description" v-show="good.description!==''">{{good.description}}</div>
                    <div class="sell">
                      <span class="sellCount">月售{{good.sellCount}}份</span>
                      <span class="rating">好评率{{good.rating}}%</span>
                    </div>
                    <div class="price-wrap">
                      <span class="price">￥</span>
                      <span class="price-num">{{good.price}}</span>
                      <span class="oldPrice" v-show="good.oldPrice!==''">￥</span>
                      <span class="oldPrice-num">{{good.oldPrice}}</span>
                    </div>
                  </div>
                </li>
              </ul>
            </li>
          </ul>
        </div>
      </div>
    </div>
    <div class="shopcart-wrap">
      <div class="shopcart-icon-wrap">
        <span class="icon-shopping_cart"></span>
      </div>
      <div class="price"></div>
      <div class="text"></div>
      <button class="btn">￥20起送</button>
    </div>
  </div>
</template>

<script>
import BScroll from 'better-scroll'
export default {
  props: {
    goods: {
      type: Array
    }
  },
  mounted() {
    this.$nextTick(() => {
      this._initBScroll()
      this.goodsRight.on('scroll', pos => {
        if (pos.y > 0) {
          this.nowIndex = 0
          this._follow(this.nowIndex)
          return
        }
        const posY = Math.abs(pos.y)
        if (posY >= this.heightArr[this.heightArr.length - 1]) {
          this.nowIndex = this.heightArr.length - 2
          this._follow(this.nowIndex)
          return
        }
        for (let i = 0, len = this.heightArr.length; i < len; i++) {
          if (posY >= this.heightArr[i] && posY < this.heightArr[i + 1]) {
            this.nowIndex = i
            this._follow(this.nowIndex)
          }
        }
      })
    })
  },
  watch: {
    goods(goods) {
      if (goods && goods.length > 0) {
        this.$nextTick(() => {
          this.heightArr = this.getListItemHeight()
        })
      }
    }
  },
  methods: {
    getListItemHeight() {
      // 获取每类食品模块的高度区间
      let heightArr = []
      const offsetTop = this.$refs.listItem[0].getBoundingClientRect().y
      for (let i = 0, len = this.$refs.listItem.length; i < len; i++) {
        heightArr.push(
          this.$refs.listItem[i].getBoundingClientRect().y - offsetTop
        )
        if (i === len - 1) {
          heightArr.push(
            this.$refs.listItem[i].getBoundingClientRect().y -
              offsetTop +
              this.$refs.listItem[i].getBoundingClientRect().height
          )
        }
      }
      return heightArr
    },
    // 匹配对应的图标样式
    mapClass(index) {
      return this.classMap[index]
    },
    _initBScroll() {
      this.goodsRight = new BScroll(this.$refs.goodsRight, {
        click: true,
        probeType: 3
      })
      this.goodsLeft = new BScroll(this.$refs.goodsLeft, {
        click: true
      })
    },
    // 让左侧侧边栏跟随滚动
    _follow(index) {
      const ele = this.$refs.leftItem[index]
      this.goodsLeft.scrollToElement(ele, 300, 0, -100)
    },
    // 点击左侧列表，高亮对应的左侧列表，并让右侧的列表滚动至对应的位置
    selFoodsItem(index, event) {
      // 原生的点击不触发（好像现在的不添加这句代码也不会触发了）
      if (!event._constructed) {
        return
      }
      // 让右侧的滚动
      const ele = this.$refs.listItem[index]
      this.goodsRight.scrollToElement(ele, 300)
    }
  },
  data() {
    return {
      classMap: ['decrease', 'discount', 'special', 'invoice', 'guarantee'],
      goodsRight: null,
      goodsLeft: null,
      heightArr: [],
      nowIndex: 0
    }
  }
}
</script>

<style lang="stylus" scoped>
@import '../../common/stylus/mixin.styl'
.goods-wrap
  position: fixed
  top: 174px
  bottom: 48px
  width: 100%
  overflow: hidden
  .goods
    display: flex
    height: 100%
    .goods-left
      flex: 0 0 80px
      width: 80px
      height: 100%
      overflow: hidden
      .list
        position: relative
        .item
          display: table
          width: 80px
          height: 54px
          box-sizing: border-box
          padding: 0 12px
          font-size: 0
          background: #f3f5f7
          &.highlight
            background: #fff
          .content
            display: table-cell
            vertical-align: middle
            bdb-1px(rgba(7, 17, 27, 0.1))
            .tag
              display: inline-block
              margin-right: 2px
              width: 12px
              height: 12px
              background-size: 12px 12px
              border-radius: 2px
              vertical-align: top
              &.decrease
                bg-image('decrease_3')
              &.discount
                bg-image('discount_3')
              &.special
                bg-image('special_3')
              &.invoice
                bg-image('invoice_3')
              &.guarantee
                bg-image('guarantee_3')
            .text
              vertical-align: top
              line-height: 14px
              font-size: 12px
              color: #07111b
    .goods-right
      flex: 1
      height: 100%
      .list
        .item
          .title
            box-sizing: border-box
            width: 100%
            height: 26px
            padding-left: 12px
            line-height: 26px
            background: #f3f5f7
            border-left: 2px solid #d9dde1
            color: #93999f
          .good-list
            .good
              display: flex
              padding: 18px 0
              margin: 0 18px
              bdb-1px(rgba(7, 17, 27, 0.1))
              &:last-child
                bdb-none()
              .icon
                flex: 0 0 57px
                width: 57px
                height: 57px
                margin-right: 9px
              .content
                flex: 1
                .name
                  margin-bottom: 8px
                  line-height: 14px
                  font-size: 14px
                  color: rgb(7, 17, 27)
                .description, .sell
                  line-height: 10px
                  margin-bottom: 8px
                  font-size: 10px
                  color: rgb(147, 153, 159)
                .sellCount
                  margin-right: 12px
                .price-wrap
                  font-size: 0
                  .price, .price-num
                    font-size: 10px
                    color: #f01414
                    vertical-align: bottom
                  .price-num
                    line-height: 14px
                    font-size: 14px
                    font-weight: bold
                    margin-right: 8px
                  .oldPrice, .oldPrice-num
                    line-height: 14px
                    font-size: 10px
                    color: rgb(143, 157, 159)
                    text-decoration: line-through
                  .oldPrice-num
                    font-weight: bold
.shopcart-wrap
  position fixed
  bottom 0
  width 100%
  height 48px
  background rgba(0,0,0,.8)
</style>
