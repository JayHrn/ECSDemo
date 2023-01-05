<template>
  <div class="container">
    <div id="MapContainer">

    </div>
    <div id="panel"></div>

    <el-button @click="driver" style="width: 20px;height: 20px;"></el-button>
    <el-input v-model="start"></el-input>
    <el-input v-model="destination"></el-input>
    <span>路费：{{this.dollar}}</span>
  </div>

</template>

<script>
import AMapLoader from '@amap/amap-jsapi-loader';

export default {
  name: "MapContainer",
  data() {
    return {
      map: null,
      dollar: '',
      start: '',
      destination: '',
      waypoints: [
        {keyword: '天津站', city: '天津'}
      ],
    }
  },
  mounted() {
    // 初始化申请key对应的秘钥，必须使用，否则无法进行路线规划
    window._AMapSecurityConfig = {
      securityJsCode: 'b53ddee9fa1fa2ddf02ec7ecf73bbbe5'
    }
    //DOM初始化完成进行地图初始化
    this.initMap();
  },

  methods: {
    initMap() {
      AMapLoader.load({
        key: "ebb44e5017076feb584c6d7871d176c0",             // 申请好的Web端开发者Key，首次调用 load 时必填
        version: "2.0",      // 指定要加载的 JSAPI 的版本，缺省时默认为 1.4.15
        plugins: ['AMap.ToolBar', 'AMap.Driving', 'AMap.AutoComplete', 'AMap.TruckDriving', 'AMap.DragRoute'],       // 需要使用的的插件列表，如比例尺'AMap.Scale'等
      }).then((AMap) => {
        this.map = new AMap.Map("MapContainer", {  //设置地图容器id
          viewMode: "3D",    //是否为3D地图模式
          zoom: 5,           //初始化地图级别
          center: [105.602725, 37.076636], //初始化地图中心点位置
          terrain: true, // 展示地形
        });
      }).catch(e => {
        console.log(e);
      })
    },
    driver() {
      let driving = new AMap.Driving({
        /* 驾车路线规划策略
         * AMap.DrivingPolicy.LEAST_TIME  //最快捷模式
         * AMap.DrivingPolicy.LEAST_FEE   //最经济模式
         * AMap.DrivingPolicy.LEAST_DISTANCE  //最短距离模式
         * AMap.DrivingPolicy.REAL_TRAFFIC  //考虑实时路况
         */
        policy: AMap.DrivingPolicy.LEAST_TIME,
        panel: 'panel',
        map: this.map,
      })
      let points = [
        // {keyword: '南昌航空大学', city: '南昌'},
        // {keyword: '天津站', city: '天津'},
        // {keyword: '亦庄文化园（地铁站）', city: '北京'}
      ]
      let startPoint={keyword: this.start,city: this.start}
      let destinationPoint={keyword: this.destination,city: this.destination}
      points.push(startPoint,destinationPoint)
      let _this=this;
      // let WayPointsOpts = {
      //   // 途经点参数，最多支持传入16个途经点
      //   waypoints: [
      //     {keyword: '杭州东站', city: '杭州'}
      //   ]
      // }
      driving.search(points, function (status, result) {
        console.log(result)
        // console.log("路费：" + result.routes[0].tolls)
        // console.log("收费路段长度：" + result.routes[0].tolls_distance)
        // console.log(result)
        // _this.dollar=result.routes[0].tolls
        // // let steps=result.steps;
        // // console.log(steps);
        // console.log(result.waypoints)
      })


      // 第二条路线
      //   let driving2 = new AMap.Driving({
      //     /* 驾车路线规划策略
      //      * AMap.DrivingPolicy.LEAST_TIME  //最快捷模式
      //      * AMap.DrivingPolicy.LEAST_FEE   //最经济模式
      //      * AMap.DrivingPolicy.LEAST_DISTANCE  //最短距离模式
      //      * AMap.DrivingPolicy.REAL_TRAFFIC  //考虑实时路况
      //      */
      //     policy: AMap.DrivingPolicy.LEAST_FEE,
      //     // panel: 'panel',
      //     map: this.map,
      //   })
      //   let points2 = [
      //     {keyword: '南昌航空大学', city: '南昌'},
      //     {keyword: '亦庄文化园（地铁站）', city: '北京'}
      //   ]
      //   var opts = {
      //     // 途经点参数，最多支持传入16个途经点
      //     waypoints: [
      //       { keyword: '北京站', city:'北京' }
      //     ]
      //   }
      //   driving2.search(points2,opts, function (status, result) {
      //     console.log("路费：" + result.routes[0].tolls)
      //     console.log("收费路段长度：" + result.routes[0].tolls_distance)
      //     console.log(result)
      //     // let steps=result.steps;
      //     // console.log(steps);
      //     console.log(result.waypoints)
      //   })
    },
  },
}
</script>

<style scoped>
.container {
  display: flex;
  justify-content: flex-start;
  width: 650px;
  height: 650px;
}

#MapContainer {
  padding: 0px;
  margin: 0px;
  width: 600px;
  height: 600px;
}
#panel{
  width: 200px;
  height: 200px;
  min-height: 200px;
}

</style>