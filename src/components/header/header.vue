<template>
  <div id="header">
    <div class="content-wrapper">
      <div class="avatar">
        <img width="64" height="64" :src="seller.avatar">
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{seller.name}}</span>
        </div>
        <div class="description">{{seller.description}}/{{seller.deliveryTime}}分钟到达</div>
        <div v-if="seller.supports" class="supports">
          <span class="supports-type" :class="classMap[seller.supports[0].type]"></span>
          <span class="supports-description">{{seller.supports[0].description}}</span>
        </div>
      </div>
      <div v-if="seller.supports" class="support-count"  @click="showDetail">
        <div class="count">{{seller.supports.length}}个</div>
        <span class="icon-keyboard_arrow_right"></span>
      </div>
    </div>
    <div class="bulletin-wrapper"  @click="showDetail">
      <span class="bulletin-title"></span><span class="bulletin-text">{{seller.bulletin}}</span>
      <span class="icon-keyboard_arrow_right"></span>
    </div>
    <div class="background">
      <img :src="seller.avatar" height="100%" width="100%"/>
    </div>
    <transition name="fade">
       <div v-show="detailShow" class="detail" >
      <div class="detail-wrapper clear-fix">
        <div class="detail-main">
          <h1 class="name">{{seller.name}}</h1>
          <star class="score" :size="48" :score="seller.score"></star>
          <div class="title">
            <div class="line"></div>
            <div class="text">优惠信息</div>
            <div class="line"></div>
          </div>
         <ul v-if="seller.supports" class="supports">
           <li class="supports-item" v-for="item in seller.supports">
             <span class="icon" :class="classMap[item.type]"></span>
             <span class="description">{{item.description}}</span>
           </li>
         </ul>
          <div class="title">
            <div class="line"></div>
            <div class="text">商家公告</div>
            <div class="line"></div>
          </div>
          <div class="bulletin-text">
            <p>{{seller.bulletin}}</p>
          </div>
        </div>
      </div>
      <div class="close" @click="hideDetail">
        <i class="icon-close"></i>
      </div>
    </div>
    </transition>
  </div>
</template>
<script type="text/ecmascript-6">
  import star from '../../components/star/star'
  export default {
    name: 'header',
    props: {
      seller: {
        type: Object
      }
    },
    data () {
      return {
        detailShow: false
      }
    },
    methods: {
      showDetail: function () {
        this.detailShow = true
      },
      hideDetail: function () {
        this.detailShow = false
      }
    },
    mounted: function () {
      this.$nextTick(() => {
        this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
      })
    },
    components: {star}
  }
</script>
<style lang="stylus" type="text/stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixin.styl"
    #header
        position relative
        overflow hidden
        color #fff
        background-color rgba(7,17,27,.5)
      .content-wrapper
        position: relative
        padding 24px 12px 18px 24px
        color #fff
        font-size 0px
        .avatar
          border-radius 2px
          overflow hidden
          display inline-block
        .content
          display inline-block
          color: #fff
          font-size 12px
          margin-left 16px
          vertical-align top
          .title
            padding 2px 0px 8px 0px
            font-size 16px
            font-weight 900
            vertical-align top
            .brand
              display inline-block
              width 30px
              height 18px
              bg-img(brand)
              background-repeat no-repeat
              background-size 30px 18px !important
              vertical-align top
          .description
            font-size 12px
            line-height 12px
            margin-bottom 10px
          .supports
            font-size 0px
            .supports-type
              vertical-align top
              display inline-block
              font-size 12px
              width 12px
              height 12px
              background-size 12px 12px !important
              background-repeat no-repeat
              &.decrease
                bg-img('decrease_1')
              &.discount
                bg-img('discount_1')
              &.guarantee
                bg-img('guarantee_1')
              &.invoice
                bg-img('invoice_1')
              &.special
                bg-img('special_1')
            .supports-description
              vertical-align top
              margin-left 4px
              font-size 12px
        .support-count
           position absolute
           right 12px
           bottom 14px
           width 32px
           height 14px
           background-color rgba(0,0,0,.2)
           border-radius 14px
           line-height 14px
           padding 4px 4px
           text-align center
           .count
             font-size 10px
             display inline-block
             vertical-align top
           .icon-keyboard_arrow_right
             display inline-block
             vertical-align top
             line-height 14px
             font-size 10px
      .bulletin-wrapper
        position relative
        height 28px
        color #fff
        background rgba(7,17,27,.2)
        padding 0px 22px 0px 12px
        line-height 28px
        white-space nowrap
        text-overflow ellipsis
        overflow hidden
        font-size 10px
        .bulletin-title
          display inline-block
          vertical-align top
          margin-top 8px
          width 22px
          height 12px
          bg-img('bulletin')
          background-size 22px 12px !important
          background-repeat no-repeat
          margin-right 4px
        .icon-keyboard_arrow_right
          display inline-block
          position: absolute
          top 9px
          right 12px
          font-size 10px
      .background
        position absolute
        left 0px
        top 0px
        z-index -1
        width 100%
        height 100%
        filter blur(10px)
      .detail
        position fixed
        top 0px
        left 0px
        width 100%
        height 100%
        overflow auto
        z-index 100
        transition all .5s
        opacity 1
        background rgba(7,17,27,.8)
        &.fade-enter,&.fade-leave-active
          opacity 0
          background rgba(7,17,27,0)
        .detail-wrapper
          min-height 100%
          width 100%
          .detail-main
            margin-top 64px
            padding-bottom 64px
            .name
              text-align center
              font-size 16px
              line-height 16px
              font-weight 700
            .score
              text-align center
              margin-top 16px
              margin-bottom 16px
            .title
              display flex
              width 80%
              margin 28px auto 18px auto
              .line
                flex 1
                position relative
                top -6px
                border-bottom 1px solid rgba(255,255,255,0.2)
              .text
                padding 0px 12px
                font-size 12px
            .supports
              width 80%
              padding 0 12px
              margin 0 auto
              font-size 0px
              .supports-item
                height 16px
                margin-bottom 12px
                &:last-child
                  margin-bottom 0
                .icon
                  display inline-block
                  width 16px
                  height 16px
                  background-size 16px 16px !important
                  vertical-align top
                  &.decrease
                    bg-img('decrease_2')
                  &.discount
                    bg-img('discount_2')
                  &.guarantee
                    bg-img('guarantee_2')
                  &.invoice
                    bg-img('invoice_2')
                  &.special
                    bg-img('special_2')

                .description
                  font-size 12px
                  line-height 16px
                  margin-left 12px
            .bulletin-text
              width 80%
              margin auto
              padding 0px 12px
              font-size 12px
              line-height 24px
        .close
          position relative
          margin -64px auto 0 auto
          font-size 32px
          clear both
          width 32px
          height 32px

</style>
