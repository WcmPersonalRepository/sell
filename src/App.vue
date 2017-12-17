<template>
  <div id="app">
    <!--<img src="./assets/logo.png">-->
    <v-header :seller="seller"></v-header>
    <!--<router-view/>-->
    <div class="tab border-1px">
      <div class="tab-item">
        <router-link to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings">评论</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/seller">商家</router-link>
      </div>
    </div>
    <router-view :seller="seller"></router-view>
  </div>
</template>

<script type="text/ecmascript-6">
  import header from './components/header/header'

  const ERRO_OK = '0'
  export default {
    name: 'app',
    data () {
      return {
        seller: {}
      }
    },
    created: function () {
      this.$http.get('../data.json').then((res) => {
        if (ERRO_OK === res.body.seller.errorno) {
          this.seller = res.body.seller
        }
      })
    },
    mounted: function () {
    },
    components: {
      'v-header': header
    }
  }
</script>

<style lang="stylus" type="text/stylus" rel="stylesheet/stylus">
  @import "common/stylus/mixin.styl"
  #app
    .tab
      display flex
      width 100%
      height 40px
      text-align center
      line-height 40px
      border-1px-bottom(rgba(7, 17, 27, .1))
      .tab-item
        flex 1
        a
          color #000
          display block
        & > .active
          color red
</style>
