<template>
  <div id="app">
    <router-link to="/qqMap">腾讯地图</router-link>
    <router-link to="/gaodeMap">高德地图</router-link>
    <router-view />
  </div>
</template>
<script>
export default {
  name: 'app',
  data() {
    return {
      longitude: 0, //经度
      latitude: 0, //纬度
      city: '',
      accuracy: 0 //误差范围
    }
  },
  methods: {},
  mounted() {}
}
</script>

<style lang="less">
body {
  height: 100%;
  font-size: 14px;
}
#app {
  font-family: 'Microsoft Yahei', 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  height: 100%;
}
a {
  padding: 5px 10px;
  border: 1px solid rgb(0, 153, 255);
  margin: 0 20px;
  color: #fff;
  background: rgb(0, 153, 255);
}
</style>
