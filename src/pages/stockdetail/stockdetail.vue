<template>

<div class="index">
    <div class = "app" id = "app" style="{height: '12.68rem', overflow: 'auto'}">
      <div class = "home">
        <stockhead :obj="stockDetail"/>
      </div>
      <mp-navbar
          v-model="activeIndex"
          :columns="columns">
        <mp-navbar-panel :active-index="activeIndex" :index="0">
          <stocktimechart/>
        </mp-navbar-panel>
        <mp-navbar-panel :active-index="activeIndex" :index="1">
          <stockklinechart/>
        </mp-navbar-panel>
        <mp-navbar-panel :active-index="activeIndex" :index="2">
          <stockklinechart/>
        </mp-navbar-panel>
        <mp-navbar-panel :active-index="activeIndex" :index="3">
          <stockklinechart/>
        </mp-navbar-panel>
      </mp-navbar>
      <stockklinechart :obj="stockDetail"/>
  </div>
</div>

</template>

<script>
import stockhead from '@/components/stockhead'
import stocktimechart from '@/components/stocktimechart'
import stockklinechart from '@/components/stockklinechart'
import { stockQuote } from '@/utils/stockapi'
import mpNavbar from 'mp-weui/packages/navbar'

export default {
  onLoad (options) {
    console.log('search:options:', options)
    this.code = options.code
    this.name = options.name
    wx.setNavigationBarTitle({
      title: this.name + '(' + this.code + ')'
    })
    stockQuote(this.code).then((res) => {
      console.log('stockQuote:res:', res[0])
      this.stockDetail = res[0]
    })
  },
  components: {
    stockhead,
    stocktimechart,
    stockklinechart,
    mpNavbar
  },
  data () {
    return {
      code: '',
      name: '',
      stockDetail: {},
      columns: ['分时', '日k', '周k', '月k'],
      activeIndex: 0
    }
  },
  methods: {
    created () {

    }
  }
}
</script>

<style scoped>
.wrap {
  width: 100%;
  height: 300px;
}
.app {
   min-height: 100vh;
   background-color: #f2f2f2;
}
.home {
  background-color: #fff;
  padding: 0.266667rem 0;
  display: flex;
  align-items: center;
}
</style>
