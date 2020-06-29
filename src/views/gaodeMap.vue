<!--  -->
<template>
  <div>
    <div id="container" style="width:600px;height:670px;margin:20px auto"></div>
    <div class="info">
      <h4 id="status"></h4>
      <hr />
      <p id="result"></p>
      <hr />
      <p>由于众多浏览器已不再支持非安全域的定位请求，为保位成功率和精度，请升级您的站点到HTTPS。</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {}
  },
  methods: {
    getGaodeMap() {
      let _that = this
      var map = new AMap.Map('container', {
        resizeEnable: true
      })
      AMap.plugin('AMap.Geolocation', function() {
        var geolocation = new AMap.Geolocation({
          enableHighAccuracy: true, //是否使用高精度定位，默认:true
          timeout: 10000, //超过10秒后停止定位，默认：5s
          buttonPosition: 'RB', //定位按钮的停靠位置
          buttonOffset: new AMap.Pixel(10, 20), //定位按钮与设置的停靠位置的偏移量，默认：Pixel(10, 20)
          zoomToAccuracy: true, //定位成功后是否自动调整地图视野到定位点
          showMarker: false, //定位成功后在定位到的位置显示点标记，默认：true
          showCircle: false //定位成功后用圆圈表示定位精度范围，默认：true  （去掉圆形区域）
        })
        map.addControl(geolocation)
        geolocation.getCurrentPosition(function(status, result) {
          if (status == 'complete') {
            onComplete(result)
          } else {
            onError(result)
          }
        })
      })
      //解析定位结果
      function onComplete(data) {
        document.getElementById('status').innerHTML = '定位成功'
        var str = []
        str.push('定位结果：' + data.position)
        console.log(data.position)
        let position = data.position
        var lnglatXY = [position.lng, position.lat]
        _that.addMarker(lnglatXY, map)
        str.push('定位类别：' + data.location_type)
        if (data.accuracy) {
          str.push('精度：' + data.accuracy + ' 米')
        } //如为IP精确定位结果则没有精度信息
        str.push('是否经过偏移：' + (data.isConverted ? '是' : '否'))
        document.getElementById('result').innerHTML = str.join('<br>')
      }
      //解析定位错误信息
      function onError(data) {
        document.getElementById('status').innerHTML = '定位失败'
        document.getElementById('result').innerHTML = '失败原因排查信息:' + data.message
      }
    },
    // 实例化点标记
    addMarker(lnglatXY, map) {
      //console.log(lnglatXY);
      let marker = null
      marker = new AMap.Marker({
        icon: 'http://webapi.amap.com/theme/v1.3/markers/n/mark_b.png',
        position: lnglatXY
      })
      marker.setMap(map)
      map.setFitView() // 执行定位
    }
  },
  mounted() {
    this.getGaodeMap()
  },
  components: {}
}
</script>
<style lang="less" scoped>
/* @import url(); 引入css类 */
</style>
