<template>
<div class = "stockhead">

  <div class = "stockhead-left">
    <div class = "stockhead-price">
      {{ price }}
    </div>
    <div class = "stockhead-text">
      {{ pc }}  {{ pcr }}
    </div>
  </div>
  <div class = "stockhead-right">
    <div>
      <p>最高</p>
    </div>
    <div class = "stockhead-text">
      {{ high }}
    </div>
    <div>
      <p>昨日</p>
    </div>
    <div class = "stockhead-text">
      {{ pre_close }}
    </div>
  </div>

  <div class = "stockhead-right">
    <div>
      <p>最低</p>
    </div>
    <div class = "stockhead-text">
      {{ low }}
    </div>
    <div>
      <p>成交量</p>
    </div>
    <div class = "stockhead-text">
      {{ volume }}
    </div>
  </div>

</div>
</template>


<script>
export default {
  props: {
    obj: Object
  },
  computed: {
    // 计算属性的 getter
    pc: function () {
      var pc = this.obj.price - this.obj.pre_close
      return pc.toFixed(2)
    },
    pcr: function () {
      var pc = this.obj.price - this.obj.pre_close
      pc = pc / this.obj.pre_close * 100
      return pc.toFixed(2) + '%'
    },
    volume: function () {
      var pc = this.obj.volume / 100
      return pc.toFixed(0)
    },
    price: function () {
      var pc = this.obj.price * 1
      return pc.toFixed(2)
    },
    high: function () {
      var pc = this.obj.high * 1
      return pc.toFixed(2)
    },
    pre_close: function () {
      var pc = this.obj.pre_close * 1
      return pc.toFixed(2)
    },
    low: function () {
      var pc = this.obj.low * 1
      return pc.toFixed(2)
    }
  }
}
</script>

<style scoped>
.stockhead {
  background-color: #fff;
  display: flex;
  flex-direction: row;
  align-items: center;
  padding: 0 0.4rem;
  font-size: 12px;
  margin-bottom: 0.1rem;
  color: #999;
  font-size: 12px;
  width: 100%;
}
.stockhead-left {
  background-color: #fff;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 0 0.4rem;
  font-size: 12px;
  margin-bottom: 0.1rem;
  color: #999;
  font-size: 12px;
}
.stockhead-right {
  background-color: #fff;
  display: flex;
  flex-direction: column;
  align-items: right;
  padding: 0 0.4rem;
  font-size: 12px;
  margin-bottom: 0.1rem;
  color: #999;
  font-size: 12px;
  flex: 1;
}
.stockhead-price {
  font-size: 25px;
  color: #000;
  font-weight: 600
}
.stockhead-text {
  color: #000;
}
</style>
