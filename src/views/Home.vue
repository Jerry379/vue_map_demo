<template>
  <div class="home">
    <baidu-map
      class="map"
      :center="center" :zoom="zoom"
      @ready="handler"
      @click="clickMap"
    >
    </baidu-map>
  </div>
</template>

<script>
import { Component, Vue } from 'vue-property-decorator';

@Component
export default class HelloWorld extends Vue {
  center =  {lng: 116.404, lat: 39.915};
  zoom = 14;
  BMap = null;
  map = null;

  handler ({BMap, map}) {
    this.BMap = BMap;
    this.map = map;
    const marker = new BMap.Marker(new BMap.Point(this.center.lng, this.center.lat));
    map.addOverlay(marker);
  }
  clickMap(e) {
    this.map.clearOverlays();
    const marker = new this.BMap.Marker(new this.BMap.Point(e.point.lng, e.point.lat));
    this.map.addOverlay(marker);
  }
}
</script>

<style lang="less" scoped>
.home{
  height: 100%;
  // overflow: scroll;//修改这里，避免内部元素发生滚动
}
.map{
  margin: 300px 0;
  width: 100%;
  height: 400px;
}
</style>
