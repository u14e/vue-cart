<template>
  <header class="header">
    <div class="content-wrapper">
      <div class="avatar">
        <img width="64" height="64" :src="seller.avatar" alt="">
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{ seller.name }}</span>
        </div>
        <div class="description">
          {{ seller.description }}/{{ seller.deliveryTime }}分钟到达
        </div>
        <div v-if="seller.supports" class="support">
          <span class="icon" :class="classMap[seller.supports[0].type]"></span>
          <span class="text">{{ seller.supports[0].description }}</span>
        </div>
      </div>
      <div v-if="seller.supports" class="support-count" @click="showDetail">
        <span class="count">{{ seller.supports.length }}个</span>
        <i class="icon-keyboard_arrow_right"></i>
      </div>
    </div>
    <div class="bulletin-wrapper" @click="showDetail">
      <span class="bulletin-title"></span>
      <span class="bulletin-text">{{ seller.bulletin }}</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>
    <div class="background">
      <img :src="seller.avatar" width="100%" height="100%" alt="">
    </div>
    <div v-show="detailShow" class="detail">
      <div class="detail-wrapper">
        <div class="detail-main">
          <p v-for="i in [1, 2, 3, 4, 5]" :key="i">{{ seller.bulletin }}</p>
        </div>
      </div>
      <div class="detail-close" @click="hideDetail">
        <i class="icon-close"></i>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: 'v-header',
  props: {
    seller: {
      type: Object,
      default: () => ({})
    }
  },
  data () {
    return {
      detailShow: true
    }
  },
  created () {
    this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
  },
  methods: {
    showDetail () {
      this.detailShow = true
    },
    hideDetail () {
      this.detailShow = false
    }
  }
}
</script>

<style lang="stylus" scoped>
@import '~styles/mixin'

.header
  position relative
  overflow hidden // 避免滤镜阴影溢出
  color #ffffff
  background-color rgba(7, 17, 27, .5)
  .content-wrapper
    position relative
    padding 24px 12px 18px 24px
    font-size 0
    .avatar
      display inline-block
      vertical-align top
      img
        border-radius 2px
    .content
      display inline-block
      margin-left 16px
      .title
        margin 2px 0 8px 0
        .brand
          display inline-block
          vertical-align top
          width 30px
          height 18px
          bg-image('./img/brand')
          background-size 30px 18px
          background-repeat no-repeat
        .name
          margin-left 6px
          font-size 16px
          line-height 18px
          font-weight bold
      .description
        margin-bottom 10px
        line-height 12px
        font-size 12px
      .support
        .icon
          display inline-block
          vertical-align top
          width 12px
          height 12px
          margin-right 4px
          background-size 12px 12px
          background-repeat no-repeat
          &.decrease
            bg-image('./img/decrease_1')
          &.discount
            bg-image('./img/discount_1')
          &.guarantee
            bg-image('./img/guarantee_1')
          &.invoice
            bg-image('./img/invoice_1')
          &.special
            bg-image('./img/special_1')
        .text
          line-height 12px
          font-size 10px
    .support-count
      position absolute
      right 12px
      bottom 12px
      padding 0 8px
      height 24px
      line-height 24px
      border-radius 14px
      background rgba(0, 0, 0, .2)
      text-align center
      .count
        vertical-align top
        font-size 10px
      i
        margin-left 2px
        line-height 24px
        font-size 10px
  .bulletin-wrapper
    position relative
    padding 0 22px 0 12px
    height 28px
    line-height 28px
    white-space nowrap
    overflow hidden
    text-overflow ellipsis
    background: rgba(7, 17, 27, 0.2)
    .bulletin-title
      display inline-block
      vertical-align top
      margin-top 8px
      width 22px
      height 12px
      bg-image('./img/bulletin')
      background-size 22px 12px
      background-repeat no-repeat
    .bulletin-text
      margin: 0 4px
      font-size 10px
    i
      position absolute
      font-size 10px    
      right 12px
      top 8px
  .background
    position absolute
    left 0
    top 0
    z-index -1
    width 100%
    height 100%
    filter blur(10px)
  .detail
    position fixed
    z-index 100    
    left 0
    top 0
    width 100%
    height 100%
    overflow auto
    background-color rgba(7, 17, 27, .8)
    .detail-wrapper
      display inline-block  // BFC
      width 100%
      min-height 100%
      .detail-main
        margin-top 64px
        padding-bottom 64px
    .detail-close
      position relative
      width 32px
      height 32px
      margin -64px auto 0
      i
        font-size 32px
</style>
