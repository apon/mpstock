<template>
  <div class="wrap">
    <mpvue-echarts :echarts="echarts" :onInit="onInit" />
  </div>
</template>

<script>

import * as echarts from 'echarts'
import mpvueEcharts from 'mpvue-echarts'
import { stockTime } from '@/utils/stockapi'

function initChart (canvas, width, height) {
  const chart = echarts.init(canvas, null, {
    width: width,
    height: height
  })
  canvas.setChart(chart)
  var option = {
    backgroundColor: '#fff',
    tooltip: {
      trigger: 'axis',
      axisPointer: {
        type: 'cross',
        animation: false,
        label: {
          backgroundColor: '#ccc',
          borderColor: '#aaa',
          borderWidth: 1,
          shadowBlur: 0,
          shadowOffsetX: 0,
          shadowOffsetY: 0,
          textStyle: {
            color: '#222'
          }
        }
      },
      formatter: function (params) {
        return params[2].name + '<br />' + params[2].value
      }
    },
    xAxis: {
      type: 'category',
      splitNumber: 3,
      max: 240,
      min: 0,
      axisLabel: {
        formatter: function (value, idx) {
          if (idx === 0) {
            return '09:30'
          }
          if (idx === 120) {
            return '11:30/13:00'
          }
          if (idx === 240) {
            return '15:00'
          }
        }
      }
    },
    yAxis: {
      show: false,
      type: 'value',
      max: 7.66,
      min: 7.18,
      splitLine: {
        show: false
      }
    },
    series: [{
      name: '',
      type: 'line',
      areaStyle: {},
      data: []
    }]
  }
  var timeData = []
  var seriesdata = []
  var min = 100000000
  var max = 0
  stockTime('600004').then((res) => {
    console.log('stockTime:', res)
    res.reverse().forEach((res) => {
      console.log('search:', res.price, res.time)
      if (res.price > max) {
        max = res.price
      }
      if (res.price < min) {
        min = res.price
      }
      seriesdata.push(res.price)
      timeData.push(res.time)
    })
    console.log('max min', max, min)
    option.series[0].data = seriesdata
    option.xAxis.data = timeData
    option.yAxis.max = max
    option.yAxis.min = min
    chart.setOption(option)
  })
  return chart
}

export default {
  components: {
    mpvueEcharts
  },
  data () {
    return {
      echarts,
      onInit: initChart
    }
  },
  props: {
    obj: Object
  },
  async onLoad () {

  }
}
</script>

<style scoped>
.wrap {
  width: 100%;
  height: 300px;
  background-color: #fff;
}
</style>
