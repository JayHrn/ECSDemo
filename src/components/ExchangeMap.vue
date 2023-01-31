<template>
  <div class="container">
    <div class="map_search">

      <div class="input-area">
        <div class="route-search-title">
          <span class="route-search-title-name">退换服务</span>
        </div>
        <!--   始发地     -->
        <div class="input-line">
          <div class="input-title">
            <span>始发地: </span>
          </div>
          <div class="input-line-clear">
            <el-cascader
                size="large"
                :options="options"
                v-model="startCity"
                placeholder="请选择始发地省市区"
                @change="selectedStartCity">
            </el-cascader>
            <el-input
                v-model="startDetail"
                placeholder="请输入始发地详细地址"
                clearable>
            </el-input>
          </div>

        </div>
        <!--   目的地     -->
        <div class="input-line">
          <div class="input-title">
            <span>目的地: </span>
          </div>
          <div class="input-line-clear">
            <el-cascader
                size="large"
                :options="options"
                v-model="destinationCity"
                placeholder="请选择省市区"
                @change="selectedDestinationCity">
            </el-cascader>
            <el-input
                v-model="destinationDetail"
                placeholder="请输入详细地址"
                clearable>
            </el-input>
          </div>
        </div>
        <div class="input-line-button">
          <el-button size="medium" plain @click="driver" type="primary">查找</el-button>
          <el-button size="medium" plain @click="drive" type="primary">开始</el-button>
        </div>
      </div>
    </div>

    <div class="map">
      <div id="MapContainer">
      </div>

      <div class="fee-container">
        <div id="panel" v-show="panelShow">
        </div>
      </div>
    </div>

  </div>

</template>

<script>
import AMapLoader from '@amap/amap-jsapi-loader';
import {regionData, CodeToText, TextToCode} from 'element-china-area-data'
import {map} from "core-js/internals/array-iteration";
// 参考资料
// https://lbs.amap.com/demo/jsapi-v2/example/marker/replaying-historical-running-data
// https://lbs.amap.com/api/jsapi-v2/documentation#markermovealong
// https://blog.csdn.net/qq_38881495/article/details/127808507
export default {
  name: "ExchangeMap",
  data() {
    return {
      marker: {},
      lineArr: [],
      speed: 1,

      map: null, //地图对象
      panelShow: false, //控制查询路线结果面板是否显示
      dollar: '', // 费用
      driving: '', //驾车对象

      // 省市区
      options: regionData,
      selectedOptions: [],

      // 起始地城市
      startCity: [],
      // 起始地具体位置
      startDetail: '',

      // 起始地城市
      destinationCity: [],
      // 起始地具体位置
      destinationDetail: '',

    }
  },
  mounted() {
    // 初始化申请key对应的秘钥，必须使用，否则无法进行路线规划
    window._AMapSecurityConfig = {
      // 1: b53ddee9fa1fa2ddf02ec7ecf73bbbe5
      // 2: 150e91861314add8330c4899a3e1823c
      securityJsCode: '150e91861314add8330c4899a3e1823c'
    }
    //DOM初始化完成进行地图初始化
    this.initMap();

  },

  methods: {
    initMap() {
      AMapLoader.load({
        // 1: ebb44e5017076feb584c6d7871d176c0
        // 2: 9560b10e33522eca4d1a6d0e5e72fa79
        key: "9560b10e33522eca4d1a6d0e5e72fa79",             // 申请好的Web端开发者Key，首次调用 load 时必填
        version: "2.0",      // 指定要加载的 JSAPI 的版本，缺省时默认为 1.4.15
        plugins: ['AMap.ToolBar', 'AMap.Driving', 'AMap.AutoComplete', 'AMap.TruckDriving', 'AMap.DragRoute', 'AMap.MoveAnimation'],       // 需要使用的的插件列表，如比例尺'AMap.Scale'等
      }).then((AMap) => {
        this.map = new AMap.Map("MapContainer", {  //设置地图容器id
          resizeEnable: true,
          center: [116.397428, 39.90923],
          zoom: 17
        });
        this.initRoad();
      }).catch(e => {
        console.log(e);
      })
    },

    // 初始化路线汽车标志
    initRoad() {
      // 初始化路径经纬度
      this.lineArr = [
        [116.478935, 39.997761],
        [116.478939, 39.997825],
        [116.478912, 39.998549],
        [116.478912, 39.998549],
        [116.478998, 39.998555],
        [116.478998, 39.998555],
        [116.479282, 39.99856],
        [116.479658, 39.998528],
        [116.480151, 39.998453],
        [116.480784, 39.998302],
        [116.480784, 39.998302],
        [116.481149, 39.998184],
        [116.481573, 39.997997],
        [116.481863, 39.997846],
        [116.482072, 39.997718],
        [116.482362, 39.997718],
        [116.483633, 39.998935],
        [116.48367, 39.998968],
        [116.484648, 39.999861]
      ];
      // 创建标记点，第一辆小汽车
      this.marker = new AMap.Marker({
        map: this.map,
        position: [116.478935, 39.997761],
        icon: "https://a.amap.com/jsapi_demos/static/demo-center-v2/car.png",
        offset: new AMap.Pixel(-13, -26),
      });

      // 小汽车还未走的路
      let polyline = new AMap.Polyline({
        map: this.map,
        path: this.lineArr,
        showDir: true,
        strokeColor: "#28F",  //线颜色
        // strokeOpacity: 1,     //线透明度
        strokeWeight: 6,      //线宽
      });
      // 小汽车已经走过的路线
      let passedPolyline = new AMap.Polyline({
        map: this.map,
        strokeColor: "#AF5",  //线颜色
        strokeWeight: 6,      //线宽
      });
      // 监听小车移动事件
      let _this = this;
      this.marker.on("moving", function (e) {
        // passedPath为Marker对象在moveAlong或者moveTo过程中已经走过的路径
        // 通过passedPath 给passedPolyline 设置path 也就是让他开始画绿色的线
        passedPolyline.setPath(e.passedPath);
        _this.map.setCenter(e.target.getPosition(), true)

        if (e.target.getPosition().lat === 39.997846 && e.target.getPosition().lng === 116.481863) {
          e.target.pauseMove();
          setTimeout(async () => {
            await e.target.resumeMove()
            await _this.anotherCar();

          }, 2000)
        }
      });
      // 让屏幕 聚焦在小汽车
      this.map.setFitView();
    },

    async anotherCar() {
      // 初始化路径经纬度
      let lineArr = [
        [116.481863, 39.997846],
        [116.481573, 39.997997],
        [116.481149, 39.998184],
        [116.480784, 39.998302],
        [116.480784, 39.998302],
        [116.480151, 39.998453],
        [116.479658, 39.998528],
        [116.479282, 39.99856],
        [116.478998, 39.998555],
        [116.478998, 39.998555],
        [116.478912, 39.998549],
        [116.478912, 39.998549],
        [116.478939, 39.997825],
        [116.478935, 39.997761],
      ];

      // 创建标记点，第一辆小汽车
      let marker = new AMap.Marker({
        map: this.map,
        position: [116.481863, 39.997846],
        icon: "https://a.amap.com/jsapi_demos/static/demo-center-v2/car.png",
        offset: new AMap.Pixel(-13, -26),
      });

      // 小汽车还未走的路
      let polyline = new AMap.Polyline({
        map: this.map,
        path: lineArr,
        showDir: true,
        strokeColor: "#28F",  //线颜色
        // strokeOpacity: 1,     //线透明度
        strokeWeight: 6,      //线宽
      });

      // 小汽车已经走过的路线
      let passedPolyline = new AMap.Polyline({
        map: this.map,
        strokeColor: "#AF5",  //线颜色
        strokeWeight: 6,      //线宽
      });

      // 监听小车移动事件
      let _this = this;
      marker.on("moving", function (e) {
        // passedPath为Marker对象在moveAlong或者moveTo过程中已经走过的路径
        // 通过passedPath 给passedPolyline 设置path 也就是让他开始画绿色的线
        passedPolyline.setPath(e.passedPath);
        _this.map.setCenter(e.target.getPosition(), true)
      });

      // 让屏幕 聚焦在小汽车

      // this.map.setFitView();

      // 第一个参数标识这个标记 移动的路径， 第二个是移动的速度
      // 第三个参数 是变化曲线函数 可以动态控制 移动速度
      marker.moveAlong(lineArr, {
        // 每一段的时长
        duration: 500,//可根据实际采集时间间隔设置
        // JSAPI2.0 是否延道路自动设置角度在 moveAlong 里设置
        autoRotation: true,
      });
    },


    drive() {
      // 第一个参数标识这个标记 移动的路径， 第二个是移动的速度
      // 第三个参数 是变化曲线函数 可以动态控制 移动速度
      this.marker.moveAlong(this.lineArr, {
        // 每一段的时长
        duration: 500,//可根据实际采集时间间隔设置
        // JSAPI2.0 是否延道路自动设置角度在 moveAlong 里设置
        autoRotation: true,
      });
    },

    driver() {
      //清除驾车路线
      if (this.driving) {
        this.driving.clear()
        this.panelShow = false
      }

      // 判断数据是否为空
      if (this.startCity.length === 0) {
        this.$message.error('起始地省市区不能为空！');
      } else if (this.startDetail === '') {
        this.$message.error('起始地详细地址不能为空！');
      } else if (this.destinationCity.length === 0) {
        this.$message.error('目的地省市区不能为空！');
      } else if (this.destinationDetail === '') {
        this.$message.error('目的地详细地址不能为空！');
      }

      if (this.startCity.length !== 0 && this.startDetail !== '' && this.destinationCity.length !== 0 && this.destinationDetail !== '') {
        let _this = this; //便于获取vue对象
        // 驾车路线规划策略
        let drivingOptions = {
          policy: this.drivePolicy,
          panel: 'panel',
          map: this.map,
        };

        // 初始化驾驶对象
        this.driving = new AMap.Driving(drivingOptions)
        // 起始点
        let startPoint = {
          keyword: this.startDetail,
          city: CodeToText[this.startCity[0]] + CodeToText[this.startCity[1]] + CodeToText[this.startCity[2]]
        }
        // 终点
        let destinationPoint = {
          keyword: this.destinationDetail,
          city: CodeToText[this.destinationCity[0]] + CodeToText[this.destinationCity[1]] + CodeToText[this.destinationCity[2]]
        }
        // 定义路径点
        let points = [];
        // 放入起点
        points.push(startPoint)
        // 放入终点
        points.push(destinationPoint)

        this.driving.search(points, function (status, result) {
          if (status === 'complete') {
            _this.panelShow = true
            _this.$notify({
              title: '成功',
              message: '查询成功',
              type: 'success',
              position: 'top-left',
            });
          } else {
            _this.$notify.error({
              title: '错误',
              message: '查询次数受限或网络不佳，线路获取失败'
            });
          }
          console.log(result)

        })
      }
    },

    selectedStartCity(location) {
      console.log("起始地城市为：" + CodeToText[location[1]])
    },
    selectedDestinationCity(location) {
      console.log("目的地城市为：" + CodeToText[location[1]])
    },
    selectedWayPointCity(location) {
      console.log("途径点城市为：" + CodeToText[location[1]])
    },
  },
}
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: flex-end;
  width: 100%;
}

.map_search {
  width: calc(100% - 600px - 2rem);
  height: calc(600px + 1.5rem);
  display: flex;
  flex-direction: column;
}

.route-search-title {
  line-height: 60px;
}

.route-search-title-name {
  display: flex;
  justify-content: center;
  font-weight: bold;
  font-size: 30px;
}

/deep/ .el-input--suffix .el-input__inner {
  padding-right: 0px;
}

.input-line {
  display: flex;
}

.input-area {
  margin: auto;
}

.input-title {
  line-height: 40px;
  width: 80px;
  text-align: right;
}

.el-cascader.el-cascader--large, .el-input.el-input--suffix {
  margin: 8px;
}

.input-line-button {
  margin-top: 10px;
  display: flex;
  justify-content: space-around;
}

/deep/ .el-select > .el-input {
  margin: 8px;
}

.map {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: flex-end;
  height: calc(600px + 1.5rem);
  align-content: space-between;
  width: calc(600px + 1.5rem);
}

#MapContainer {
  padding: 0;
  margin: 0;
  width: calc(600px + 1.5rem);
  height: calc(600px + 1.5rem);
  border-radius: 8px;
  position: relative;
}


/*前往百度地图消失*/
/deep/ .amap-call {
  display: none !important;
}

/deep/ dl.plan.plan-nobus {
  background: rgba(255, 255, 255);
}


/deep/ .fee-container {
  position: absolute;
  width: calc(250px + 1rem);
  height: calc(600px + 1.5rem);
  top: 100px;
  border-radius: 8px;
  display: flex;
  overflow: auto;
  flex-wrap: wrap;
}

.fee {
  z-index: 99;
  background-color: #ffffff;
  color: #565656;
  width: 100%;
  font-size: 14px;
  border: 1px solid silver;
  text-align: center;
  border-radius: 8px 0 0 0;
  font-weight: bold;
  position: absolute;
}

#panel {
  /*position: absolute;*/
  /*width: calc(250px + 1rem);*/
  /*height: calc(600px + 1.5rem);*/
  /*top: 100px;*/
  /*border-radius: 8px;*/
  /*display: flex;*/
  /*overflow: auto;*/
  /*flex-wrap: wrap;*/
}

/* 表单区域 */
/deep/ .el-form-item__content {
  display: flex;
  align-items: center;
}


</style>