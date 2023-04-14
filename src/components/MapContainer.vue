<template>
  <div id="container"></div>
</template>

<script>
import AMapLoader from '@amap/amap-jsapi-loader'
import { shallowRef } from '@vue/reactivity'
window._AMapSecurityConfig = {
  securityJsCode: ''
}
export default {
  setup () {
    const map = shallowRef(null)
    return {
      map
    }
  },
  methods: {
    initMap () {
      AMapLoader.load({
        key: '', // 申请好的Web端开发者Key，首次调用 load 时必填
        version: '2.0', // 指定要加载的 JSAPI 的版本，缺省时默认为 1.4.15
        plugins: ['AMap.Geolocation'] // 需要使用的的插件列表，如比例尺'AMap.Scale'等
      })
        .then((AMap) => {
          this.map = new AMap.Map('container', {
            // 设置地图容器id
            viewMode: '3D', // 是否为3D地图模式
            zoom: 15, // 初始化地图级别
            center: [114.059563, 22.54286] // 初始化地图中心点位置
          })
          const marker = new AMap.Marker({
            position: new AMap.LngLat(114.059563, 22.54286), // 经纬度对象，也可以是经纬度构成的一维数组[116.39, 39.9]
            title: '餐饮'
          })
          this.map.add(marker)
        })
        .catch((e) => {
          console.log(e)
        })
    }
    // 创建一个 Marker 实例：
  },
  mounted () {
    // DOM初始化完成进行地图初始化
    this.initMap()
  }
}
</script>

<style scoped>
#container {
  padding: 0px;
  margin: 0px;
  width: 100%;
  height: 800px;
}
</style>
