<template>
  <div id='goods'>
    <div class="menu-wrapper" ref="menuWrapper">
      <ul v-if="goods" class="menus">
        <li v-for="(item,index) in goods" @click="selectMenu(index,$event)" class="menu-item border-1px"
            :class="{current:calculateIndex==index }">
          <span class="text"><supports v-if="item.type>-1" :index="2" :type="item.type" class="icon"></supports>{{item.name}}</span>
        </li>
      </ul>
    </div>
    <div class="foods-wrapper" ref="foodsWrapper">
      <ul class="foods">
        <li class="foods-item" v-for="item in goods">
          <div class="title">
            <h1 class="name">{{item.name}}</h1>
          </div>
          <div v-for="food in item.foods" class="foods border-1px">
            <div class="icon">
              <img width="57" height="57" :src="food.icon"/>
            </div>
            <div class="foods-detail">
              <h1 class="name">{{food.name}}</h1>
              <div class="description" v-if="food.description">{{food.description}}</div>
              <div class="count">
                <span class="sell-count">月售{{food.sellCount}}份</span><span class="rating">好评率{{food.rating}}%</span>
              </div>
              <div class="price">
                <span class="now-price">￥{{food.price}}</span><span v-if="food.oldPrice" class="old-price">￥{{food.oldPrice}}</span>
              </div>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  import supports from '../supports/supports.vue'
  import BScroll from 'better-scroll'

  const EERO_OK = '0'
  export default {
    name: 'goods',
    data: function () {
      return {
        goods: [],
        seller: {},
        heightArr: [],
        scrollY: 0
      }
    },
    computed: {
      calculateIndex: function () {
        for (let i = 0; i < this.heightArr.length; i++) {
          let h1 = this.heightArr[i]
          let h2 = this.heightArr[i + 1]
          if (!h2 || (this.scrollY >= h1 && this.scrollY < h2)) {
            return i
          }
        }
        return 0
      }
    },
    mounted: function () {
      this.$http.get('../../data.json').then(function (res) {
        if (EERO_OK === res.body.errorno) {
          this.goods = res.body.goods
          this.seller = res.body.seller
          this.$nextTick(() => {
            this._calculateListHeight()
            this._initScroll()
          })
        }
      })
    },
    methods: {
      _initScroll: function () {
        this.menuScroll = new BScroll(this.$refs.menuWrapper, {
          click: true
        })
        this.foodScroll = new BScroll(this.$refs.foodsWrapper, {
          probeType: 3
        })
        this.foodScroll.on('scroll', (pos) => {
          this.scrollY = Math.abs(Math.round(pos.y))
        })
      },
      _calculateListHeight: function () {
        let foodsItem = this.$refs.foodsWrapper.getElementsByClassName('foods-item')
        let height = 0
        this.heightArr.push(height)
        for (let i = 0; i < foodsItem.length; i++) {
          height += foodsItem[i].clientHeight
          this.heightArr.push(height)
        }
      },
      selectMenu: function (index, event) {
        if (!event._constructed) {
          return
        }
        let foodsItem = this.$refs.foodsWrapper.getElementsByClassName('foods-item')
        let el = foodsItem[index]
        this.foodScroll.scrollToElement(el, 300)
      }
    },
    components: {
      supports
    }
  }
</script>

<style lang="stylus" type="text/stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixin.styl"
  #goods
    position absolute
    top 174px
    bottom 64px
    width 100%
    display flex
    overflow hidden
    .menu-wrapper
      flex 0 0 80px
      background-color #f3f5f7
      width 80px
      position relative
      .menus
        width 80px
        .menu-item
          display table
          padding 0 12px
          height 54px
          width 100%
          font-size 12px
          line-height 14px
          box-sizing border-box
          border-1px-bottom(rgba(7, 17, 27, .1))
          &.current
            font-weight 700
            border-left 2px solid dodgerblue
            margin-top -1px
            background-color #fff
            border-none()
          &:last-child
            border-none()
          .icon
            vertical-align top
            margin-right 2px
          .text
            display table-cell
            width 56px
            vertical-align middle
    .foods-wrapper
      flex 1
      font-size 12px
      .foods
        width 100%
        .foods-item
          width 100%
          .title
            width 100%
            height 26px
            line-height 26px
            color rgb(147, 153, 159)
            padding-left 14px
            border-left 1px solid #d9dde1
            background-color #f3f5f7
          .foods
            display flex
            padding 18px 0
            margin 0 18px
            border-1px-bottom(rgba(7, 17, 27, .1))
            &:last-child
              border-none()
            .icon
              flex 0 0 57px
            .foods-detail
              flex 1
              margin-left 10px
              .name
                font-size 14px
                line-height 14px
                color rgb(7, 17, 27)
                padding 4px 0
              .description, .count
                font-size 10px
                padding 4px 0px
                line-height 10px
                color rgb(147, 153, 159)
                .rating
                  margin-left 12px
              .price
                font-size 10px
                .now-price
                  font-size 14px
                  line-height 14px
                  color rgb(240, 20, 20)
                  font-weight 700
                .old-price
                  text-decoration line-through
                  line-height 10px
                  color rgb(147, 153, 159)
                  margin-left 8px
                  font-weight 700
</style>
