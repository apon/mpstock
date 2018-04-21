<template>
  <div class="wrap">
    <mpvue-echarts :echarts="echarts" :onInit="onInit" :lazyLoad="lazyLoad"/>
  </div>
</template>

<script>

import * as echarts from 'echarts'
import mpvueEcharts from 'mpvue-echarts'
import { stockKData } from '@/utils/stockapi'

function initChart (canvas, width, height) {
  const chart = echarts.init(canvas, null, {
    width: width,
    height: height
  })
  canvas.setChart(chart)
  var upColor = '#ec0000'
  var upBorderColor = '#8A0000'
  var downColor = '#00da3c'
  var downBorderColor = '#008F28'
  var option = {
    backgroundColor: '#fff',
    tooltip: {
      trigger: 'axis',
      axisPointer: {
        type: 'cross'
      }
    },
    xAxis: {
      type: 'category',
      data: [],
      scale: true,
      boundaryGap: false,
      axisLine: {onZero: false},
      splitLine: {show: false},
      splitNumber: 20,
      min: 'dataMin',
      max: 'dataMax'
    },
    yAxis: {
      scale: true,
      splitArea: {
        show: false
      }
    },
    dataZoom: [
      {
        type: 'inside',
        start: 90,
        end: 100
      }
    ],
    series: [{
      name: '',
      type: 'candlestick',
      data: [],
      itemStyle: {
        normal: {
          color: upColor,
          color0: downColor,
          borderColor: upBorderColor,
          borderColor0: downBorderColor
        }
      }},
    {
      name: 'MA5',
      type: 'line',
      data: [],
      smooth: true,
      lineStyle: {
        normal: {opacity: 0.5}
      }
    },
    {
      name: 'MA10',
      type: 'line',
      data: [],
      smooth: true,
      lineStyle: {
        normal: {opacity: 0.5}
      }
    },
    {
      name: 'MA20',
      type: 'line',
      data: [],
      smooth: true,
      lineStyle: {
        normal: {opacity: 0.5}
      }
    }
    ]
  }
  var timeData = []
  var seriesdata = []
  stockKData('600004').then((res) => {
    console.log('stockKData:', res)
    res.forEach((res) => {
      var kd = [res.open, res.close, res.low, res.high]
      seriesdata.push(kd)
      timeData.push(res.date)
    })
    option.series[0].data = seriesdata
    option.series[1].data = calculateMA(5, seriesdata)
    option.series[2].data = calculateMA(10, seriesdata)
    option.series[3].data = calculateMA(20, seriesdata)
    option.xAxis.data = timeData
    chart.setOption(option)
  })
  return chart
}

function calculateMA (dayCount, seriesdata) {
  var result = []
  for (var i = 0, len = seriesdata.length; i < len; i++) {
    if (i < dayCount) {
      result.push('-')
      continue
    }
    var sum = 0
    for (var j = 0; j < dayCount; j++) {
      sum += seriesdata[i - j][1]
    }
    result.push(sum / dayCount)
  }
  return result
}

export default {
  components: {
    mpvueEcharts
  },
  data () {
    return {
      echarts,
      lazyLoad: true,
      onInit: initChart
    }
  },
  props: {
    obj: Object
  },
  watch: {
    obj: {
      deep: true,
      handler () {
        this.$children[0].init()
        console.log('stockKData:init', this.obj)
      }
    }
  },
  methods: {
    init () {
      // this.$children[0].init()
    }
  },
  async onLoad () {
    // this.init()
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
