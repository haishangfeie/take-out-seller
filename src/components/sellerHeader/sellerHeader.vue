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
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    mapClass (index) {
      return this.classMap[index]
    }
  },
  data () {
    return {
      classMap: ['decrease', 'discount', 'special', 'invoice', 'guarantee']
    }
  },
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
@import '../../common/stylus/mixin.styl';

.header {
  position: relative;
  display: flex;
  box-sizing: border-box;
  width: 100%;
  height: 134px;
  padding: 24px 0 0 24px;
  background: #ccc;

  .header-left {
    flex: 0 0 64px;
    width: 64px;
    height: 64px;
    margin-right: 16px;

    .avatar {
      border-radius: 2px;
    }
  }

  .header-right {
    flex: 1;

    .title-warp {
      font-size: 0;

      .brand, .title {
        display: inline-block;
        vertical-align: top;
      }

      .brand {
        width: 30px;
        height: 18px;
        background-size: 30px 18px;
        bg-image('brand');
        border-radius: 2px;
      }

      .title {
        margin-left: 6px;
        margin-bottom: 8px;
        line-height: 18px;
        font-size: 16px;
        font-weight: bold;
        color: #fff;
      }
    }

    .desc {
      margin-bottom: 10px;
      line-height: 12px;
      font-size: 12px;
      color: #fff;
    }

    .supports {
      font-size: 0;

      .tag {
        display: inline-block;
        margin-right: 4px;
        width: 12px;
        height: 12px;
        background-size: 12px 12px;
        border-radius: 2px;

        &.decrease {
          bg-image('decrease_1');
        }

        &.discount {
          bg-image('discount_1');
        }

        &.special {
          bg-image('special_1');
        }

        &.invoice {
          bg-image('invoice_1');
        }

        &.guarantee {
          bg-image('guarantee_1');
        }
      }

      .description {
        vertical-align: top;
        line-height: 12px;
        font-size: 10px;
        color: #fff;
      }
    }
  }

  .bulletin {
    position: absolute;
    left: 0;
    bottom: 0;
    display: flex;
    width: 100%;
    height: 28px;
    background: rgba(7, 17, 27, 0.2);

    .bulletin-img {
      flex: 0 0 22px;
      width: 22px;
      height: 12px;
      margin: 8px 4px 8px 12px;
      background-size: 22px 12px;
      bg-image('bulletin');
    }

    .text {
      margin-right: 20px;
      flex: 1;
      height: 28px;
      line-height: 28px;
      font-size: 10px;
      color: #fff;
      // 超出字隐藏
      overflow: hidden;
      white-space:nowrap
      text-overflow:ellipsis

    }
  }
}
</style>
