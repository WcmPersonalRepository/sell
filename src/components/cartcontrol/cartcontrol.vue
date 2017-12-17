<template>
  <div class="cart-control">
    <transition name="fade">
      <div class="cart-decrease" @click="decreaseCart" v-show="food.count">
        <transition name="rotate">
          <div class="inner icon-remove_circle_outline" v-show="food.count"></div>
        </transition>
      </div>
    </transition>
    <div class="cart-count" v-show="food.count">{{food.count}}</div>
    <div class="cart-add icon-add_circle" @click="addCart"></div>
  </div>
</template>

<script type="text/ecmascript-6">
  import Vue from 'vue'

  export default {
    props: {
      food: {
        type: Object
      }
    },
    created: function () {
      Vue.set(this.food, 'count', 0)
    },
    methods: {
      addCart: function (event) {
        if (!event._constructed) {
          return
        }
        this.food.count++
      },
      decreaseCart: function (event) {
        if (!event._constructed) {
          return
        }
        this.food.count--
      }
    }
  }
</script>

<style lang="stylus" type="text/stylus" rel="stylesheet/stylus">
  .cart-control
    font-size 0
    .cart-decrease
      display: inline-block
      .inner
        display: inline-block
        font-size 24px
        line-height 24px
        color rgb(0, 160, 220)
        padding 6px
        &.rotate-enter-active,.rotate-leave-active
          transition all .5s
        &.rotate-enter,.rotate-leave-to
          transform rotate(180deg)
      &.fade-enter-active, .fade-leave-active
        transition all .5s
      &.fade-enter,.fade-leave-to
        opacity 0
        transform translate3D(48px, 0, 0)
    .cart-count
      display inline-block
      width 24px
      vertical-align top
      line-height 24px
      font-size 10px
      color rgb(147, 153, 159)
      margin-top 6px
      text-align center
    .cart-add
      display: inline-block
      font-size 24px
      line-height 24px
      color rgb(0, 160, 220)
      padding 6px
</style>
