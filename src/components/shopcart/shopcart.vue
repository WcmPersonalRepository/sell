<template>
  <div class="shop-cart">
    <div class="left">
      <div class="shop-cart-logo">
        <div class="num" v-show="totalCount">{{totalCount}}</div>
        <i class="icon-shopping_cart" :class="{'hight-light':totalCount>0}"></i>
      </div>
      <div class="total-price" :class="{'hight-light':totalPrice>0}">￥{{totalPrice}}</div>
      <div class="deliveryPrice">另需配送费{{deliveryPrice}}元</div>
    </div>
    <div class="right" :class="{'hight-light':isGoShop}">{{description}}</div>
  </div>
</template>

<script type="text/ecmascript-6">
  export default {
    props: {
      deliveryPrice: {
        type: Number,
        default: 0
      },
      minPrice: {
        type: Number,
        default: 0
      },
      selectFoods: {
        type: Array,
        default: function () {
          return [
            {
              price: 10,
              count: 1
            }
          ]
        }
      }
    },
    computed: {
      totalPrice: function () {
        let total = 0
        this.selectFoods.forEach((food) => {
          total += food.price * food.count
        })
        return total
      },
      totalCount: function () {
        let count = 0
        this.selectFoods.forEach((food) => {
          count += food.count
        })
        return count
      },
      isGoShop: function () {
        let diff = this.minPrice - this.totalPrice
        return diff <= 0
      },
      description: function () {
        let desc = `￥${this.minPrice}起送`
        let diff = this.minPrice - this.totalPrice
        if (diff <= 0) {
          desc = `去结算`
        }
        if (diff > 0 && diff < this.minPrice) {
          desc = `还差￥${diff}起送`
        }
        if (diff === this.minPrice) {
          desc = `￥${this.minPrice}起送`
        }
        return desc
      }
    }
  }
</script>

<style lang="stylus" type="text/stylus" rel="stylesheet/stylus">
  .shop-cart
    position fixed
    display flex
    left 0px
    bottom 0px
    width 100%
    height 48px
    background-color #141d27
    z-index 50
    .left
      flex 1
      font-size 0
      .shop-cart-logo
        position relative
        display inline-block
        width 50px
        height 50px
        background-color #141d27
        padding 6px
        border-radius 50%
        margin -8px 18px 0 18px
        box-sizing border-box
        .num
          position absolute
          top 0px
          right 0px
          font-size 9px
          width 24px
          height 16px
          line-height 16px
          text-align center
          color #fff
          border-radius 16px
          background-color rgb(240, 20, 20)
          box-shadow 0 4px 8px 0 rgba(0, 0, 0, .4)
        .icon-shopping_cart
          display block
          width 100%
          height 100%
          background-color rgba(255, 255, 255, .2)
          border-radius 50%
          color rgba(255, 255, 255, .4)
          line-height 42px
          text-align center
          font-size 24px
          &.hight-light
            background-color #0099cc
            color #fff
      .total-price
        display inline-block
        font-size 16px
        font-weight 700
        color rgba(255, 255, 255, .4)
        height 24px
        margin 12px 0px
        line-height 24px
        padding-right 12px
        border-right 1px solid rgba(255, 255, 255, .1)
        &.hight-light
          color #fff
      .deliveryPrice
        display inline-block
        font-size 14px
        color rgba(255, 255, 255, .4)
        line-height 48px
        margin-left 12px
    .right
      flex 0 0 105px
      background-color rgba(255, 255, 255, .1)
      color rgba(255, 255, 255, .4)
      font-size 14px
      font-weight 700
      line-height 48px
      text-align center
      &.hight-light
        color #fff
        background-color #00cc33
</style>
