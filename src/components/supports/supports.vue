<template>
  <div id="supports" :class="classMap[index][type]">

  </div>
</template>

<script type="text/ecmascript-6">
  export default {
    props: {
      index: {
        type: Number
      },
      type: {
        type: Number
      }
    },
    created: function () {
      this.classMap = [
        ['decrease_1', 'discount_1', 'special_1', 'invoice_1', 'guarantee_1'],
        ['decrease_2', 'discount_2', 'special_2', 'invoice_2', 'guarantee_2'],
        ['decrease_3', 'discount_3', 'special_3', 'invoice_3', 'guarantee_3'],
        ['decrease_4', 'discount_4', 'special_4', 'invoice_4', 'guarantee_4']
      ]
    }
  }
</script>

<style lang="stylus" type="text/stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixin.styl"
  #supports
    display inline-block
    background-repeat no-repeat !important
    &.decrease_1
      width 12px
      height 12px
      bg-img("decrease_1")
      background-size 12px 12px !important
    &.discount_1
      width 12px
      height 12px
      bg-img("discount_1")
      background-size 12px 12px !important
    &.special_1
      width 12px
      height 12px
      bg-img("special_1")
      background-size 12px 12px !important
    &.invoice_1
      width 12px
      height 12px
      bg-img("invoice_1")
      background-size 12px 12px !important
    &.guarantee_1
      width 12px
      height 12px
      bg-img("guarantee_1")
      background-size 12px 12px !important
    &.decrease_2
      width 16px
      height 16px
      bg-img("decrease_2")
      background-size 16px 16px !important
    &.discount_2
      width 16px
      height 16px
      bg-img("discount_2")
      background-size 16px 16px !important
    &.special_2
      width 16px
      height 16px
      bg-img("special_2")
      background-size 16px 16px !important
    &.invoice_2
      width 16px
      height 16px
      bg-img("invoice_2")
      background-size 16px 16px !important
    &.guarantee_2
      width 16px
      height 16px
      bg-img("guarantee_2")
      background-size 16px 16px !important
    &.decrease_3
      width 12px
      height 12px
      bg-img("decrease_3")
      background-size 12px 12px !important
    &.discount_3
      width 12px
      height 12px
      bg-img("discount_3")
      background-size 12px 12px !important
    &.special_3
      width 12px
      height 12px
      bg-img("special_3")
      background-size 12px 12px !important
    &.invoice_3
      width 12px
      height 12px
      bg-img("invoice_3")
      background-size 12px 12px !important
    &.guarantee_3
      width 12px
      height 12px
      bg-img("guarantee_3")
      background-size 12px 12px !important
    &.decrease_4
      width 16px
      height 16px
      bg-img("decrease_4")
      background-size 16px 16px !important
    &.discount_4
      width 16px
      height 16px
      bg-img("discount_4")
      background-size 16px 16px !important
    &.special_4
      width 16px
      height 16px
      bg-img("special_4")
      background-size 16px 16px !important
    &.invoice_4
      width 16px
      height 16px
      bg-img("invoice_4")
      background-size 16px 16px !important
    &.guarantee_4
      width 16px
      height 16px
      bg-img("guarantee_4")
      background-size 16px 16px !important

</style>
