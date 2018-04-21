<template>
  <div class="index">
      <div class = "app" id = "app" style="{height: '12.68rem', overflow: 'auto'}">
          <div class = "home">
              <div class = "home-search">
                  <i class = "iconfont icon-search"></i>
                <input type = "text" v-model = "value" placeholder = "输入股票代码搜索个股"/>
              </div>
        </div>
        <div class = "home-content">
              <p class = "nodata" v-if = "stockArr.length === 0 ">暂无数据</p>
              <div @click="goStockDetail(item)" v-for = "(item ,index) in stockArr" :key = "index">
                  <stockcard :obj = "item"></stockcard>
              </div>
        </div>
    </div>
  </div>
</template>

<script>
import stockcard from '@/components/stockcard'
import { searchStock } from '@/utils/stockapi'
export default {
  name: 'article',
  data () {
    return {
      value: '',
      stockArr: [],
      userInfo: {}
    }
  },

  components: {
    stockcard
  },

  methods: {
    goStockDetail (obj) {
      var code = obj.code
      var name = obj.name
      wx.navigateTo({
        url: '/pages/stockdetail/main?code=' + code + '&name=' + name
      })
    }
  },
  watch: {
    value: function (val) {
      if (val.length < 3) {
        return
      }
      wx.showLoading()
      searchStock(val).then((res) => {
        console.log('search:', res)
        this.stockArr = res
        wx.hideLoading()
      })
    }
  }
}
</script>

<style scoped>
/*home 首页*/
.app {
   min-height: 100vh;
   background-color: #f2f2f2;
}
.home {
  background-color: #f2f2f2;
  padding: 0.266667rem 0;
  display: flex;
  align-items: center;
}
.home-search {
  height: 0.746667rem;
  margin-left: 0.2rem;
  margin-right:  0.2rem;
  display: flex;
  align-items: center;
  background-color: #fff;
  flex:1;
  border-radius: 0.133333rem;
}
.home-search input{
  width: 100%;
  /*height: 0.28rem;*/
  margin-left: 0.1rem;
  font-size: 12px;
}
.home-search input::-webkit-input-placeholder {
  color: #999;
  line-height: 0.466667rem;
}
.home-search i {
  margin-left: 0.266667rem;
}
.nodata {
	font-size: 24rpx;
	text-align: center;
}
</style>
