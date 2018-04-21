<template>
<div class = "stockcard">
    <div>
      <div class = "stockcard-content-name">
        {{ obj.name }}
      </div>
      <div class = "stockcard-content-code">
        {{ obj.code }}
      </div>
    </div>
    <div class = "stockcard-content-price">
      {{ obj.open }}
    </div>
    <div class = "stockcard-content-rate">
      {{ obj.change + "%" }}
    </div>
  </div>
</template>

<script>
export default {
  props: {
    obj: Object
  }
}
</script>

<style scoped>
/*stockcard 组件*/
.stockcard {
  background-color: #fff;
  display: flex;
  flex-direction: row;
  align-items: center;
  padding: 0 0.4rem;
  font-size: 12px;
  margin-bottom: 0.1rem;
  color: #999;
  font-size: 12px;
}
.stockcard-content-name {
  font-size: 14px;
  margin-top: 0.233333rem;
  width: 4rem;
  overflow: hidden;
  word-break: keep-all;
  white-space: nowrap;
  text-overflow: ellipsis;
  color: #333;
  font-size: 14px;
  font-weight: 600
}
.stockcard-content-code {
  padding-bottom: 0.2rem;
}
.stockcard-content-price {
  width: 4rem;
  overflow: hidden;
  word-break: keep-all;
  white-space: nowrap;
  text-overflow: ellipsis;
  color: green;
  font-size: 14px;
  font-weight: 600
}
.stockcard-content-rate {
  margin: 0.263333rem 0;
  font-size: 12px;
  color: green;
}


</style>
