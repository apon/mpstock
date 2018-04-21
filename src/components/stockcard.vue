<template>
<div class = "stockcard">
          <div class = "stockcard-content-name">
            {{ obj.name }}
          </div>
          <div>
            {{ obj.code }}
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
  align-items: center;
  padding: 0 0.4rem;
  align-items: center;
  font-size: 12px;
  margin-bottom: 0.1rem;
  color: #999;
  font-size: 12px;
  width: 100%;
}
.stockcard-content-name {
  font-size: 14px;
  margin-top: 0.233333rem;
  margin-bottom: 0.233333rem;
  width: 4rem;
  overflow: hidden;
  word-break: keep-all;
  white-space: nowrap;
  text-overflow: ellipsis;
  color: #333;
  font-size: 14px;
  font-weight: 600
}

</style>
