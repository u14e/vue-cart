<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="tab">
      <div class="tab-item">
        <router-link :to="{ name: 'goods' }">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link :to="{ name: 'ratings' }">评价</router-link>
      </div>
      <div class="tab-item">
        <router-link :to="{ name: 'seller' }">商家</router-link>        
      </div>
    </div>
    <router-view></router-view>
  </div>
</template>

<script>
import VHeader from 'components/header/header'
import axios from 'axios'

const ERR_OK = 0

export default {
  name: 'App',
  data () {
    return {
      seller: {}
    }
  },
  components: {
    [VHeader.name]: VHeader
  },
  created () {
    axios.get('/api/seller')
      .then(res => {
        const data = res.data
        if (data.errno === ERR_OK) {
          this.seller = data.data
        } else {
          console.error('error')
        }
      })
  }
}
</script>

<style lang="stylus">
@import '~styles/mixin'

#app
  .tab
    display flex
    width 100%
    height 40px
    line-height 40px
    border-1px(rgba(7, 17, 27, .1))
    .tab-item
      flex 1
      text-align center
      > a
        display block
        font-size 14px
        color rgb(77, 85, 93)
        &.active
          color rgb(240, 20, 20)
</style>
