<template>
  <div id="app">
    <router-view></router-view> 
    <picshow style="dsds:dsdsds;" 
      :imgUrlarr="imgArr" 
      :time="300" 
      @gy_click="test"
    />
    <searchbox />
    <buttonbar />
  </div>
</template>

<script>
// 资源包的导入和图片的引入
import picshow from '../components/picshow.vue'
import searchbox from '../components/seachbar.vue'
import buttonbar from '../components/buttonbar.vue'

export default {
  name: 'app',
  data(){
    return {
      // 轮播图图片插入
      imgArr:[require("../image/picshow/0.jpg"),require("../image/picshow/1.jpg"),require("../image/picshow/2.jpg")]
    }
  },
  // 方法集合
  methods:{
  },
  components: {
    picshow,
    searchbox,
    buttonbar
  }
}
</script>

<style>
  body {
    position: relative;
    margin: 0;
  }
</style>
