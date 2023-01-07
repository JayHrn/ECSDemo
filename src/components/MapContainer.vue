<template>
  <div class="container">
    <div class="map_search">

      <div class="input-area">
        <div class="route-search-title">
          <span class="route-search-title-name">路线规划</span>
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

        <div class="input-line">
          <div class="input-title">
            <span>驾车策略: </span>
          </div>
          <div class="input-line-clear">
            <el-select v-model="drivePolicy" clearable placeholder="默认最快捷模式">
              <el-option
                  v-for="item in drivePolicyOptions"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value">
              </el-option>
            </el-select>
          </div>
        </div>

        <div class="input-line-button">
          <el-button size="medium" @click="wayPointsDialogVisible=true" type="primary">添加途径点</el-button>
          <el-button size="medium" plain @click="driver" type="primary">查找</el-button>
        </div>

      </div>
    </div>

    <div class="map">
      <div id="MapContainer">
      </div>

      <div class="fee-container">
        <div class="fee" v-show="panelShow">路费：{{ dollar }}元</div>
        <div id="panel" v-show="panelShow">
        </div>

      </div>
    </div>
    <!--        添加途径点-->
    <el-dialog
        title="添加途径点"
        :visible.sync="wayPointsDialogVisible"
        width="50%"
        center>

      <el-form :model="dynamicValidateForm" ref="dynamicValidateForm" label-width="100px" class="WayPoints-dynamic">
        <el-form-item
            v-for="(wayPoint, index) in dynamicValidateForm.wayPoints"
            :label="'途径点' + (index+1)"
            :key="wayPoint.key"
        >
          <el-cascader
              size="large"
              :options="options"
              v-model="wayPoint.city"
              placeholder="请选择省市区"
              @change="selectedWayPointCity">
          </el-cascader>
          <el-input
              v-model="wayPoint.detailLocation"
              placeholder="请输入详细地址"
              clearable>
          </el-input>
          <el-button @click.prevent="removeWayPoint(wayPoint)">删除</el-button>
        </el-form-item>

        <el-form-item>
          <el-button @click="addWayPoint">新增途径点</el-button>
          <el-button @click="wayPointsDialogVisible = false">取 消</el-button>
          <el-button type="primary" @click="submitForm('dynamicValidateForm'), wayPointsDialogVisible = false ">确定
          </el-button>

        </el-form-item>
      </el-form>
    </el-dialog>
  </div>

</template>

<script>
import AMapLoader from '@amap/amap-jsapi-loader';
import {regionData, CodeToText, TextToCode} from 'element-china-area-data'
import {map} from "core-js/internals/array-iteration";

export default {
  name: "MapContainer",
  data() {
    return {
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

      // 驾车策略，select框
      drivePolicyOptions: [{
        value: 'AMap.DrivingPolicy.LEAST_TIME',
        label: '最快捷模式'
      }, {
        value: 'AMap.DrivingPolicy.LEAST_FEE',
        label: '最经济模式'
      }, {
        value: 'AMap.DrivingPolicy.LEAST_DISTANCE',
        label: '最短距离模式'
      }, {
        value: 'AMap.DrivingPolicy.REAL_TRAFFIC',
        label: '考虑实时路况'
      }],
      // 获取驾车策略选中值
      drivePolicy: '',

      // 途径点对话框
      wayPointsDialogVisible: false,
      // 添加途径点表单
      dynamicValidateForm: {
        wayPoints: [{
          city: [],
          detailLocation: '',
        }],
      }
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
        plugins: ['AMap.ToolBar', 'AMap.Driving', 'AMap.AutoComplete', 'AMap.TruckDriving', 'AMap.DragRoute'],       // 需要使用的的插件列表，如比例尺'AMap.Scale'等
      }).then((AMap) => {
        this.map = new AMap.Map("MapContainer", {  //设置地图容器id
          rotateEnable: true,
          pitchEnable: true,
          pitch: 50,
          rotation: -15,
          viewMode: "3D",    //是否为3D地图模式
          zoom: 10,           //初始化地图级别，初始放大的程度
          // center: [115.94422, 28.54538], //初始化地图中心点位置
          terrain: true, // 展示地形
        });
        // 设置地图初始化为你所在的城市
        map.getCity(function (info) {
          // var node = new PrettyJSON.view.Node({
          //   el: document.querySelector("#map-city"),
          //   data: info
          // });
        });
      }).catch(e => {
        console.log(e);
      })
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
        // 放入途径点
        if (this.dynamicValidateForm.wayPoints[0].detailLocation !== '') { //为了判断是否有途径点
          for (let i = 0; i < this.dynamicValidateForm.wayPoints.length; i++) {
            let point = this.dynamicValidateForm.wayPoints[i];
            points.push({
              keyword: point.detailLocation,
              city: CodeToText[point.city[0]] + CodeToText[point.city[1]] + CodeToText[point.city[2]]
            })
          }
        }
        // 放入终点
        points.push(destinationPoint)

        this.driving.search(points, function (status, result) {
          if (status === 'complete') {
            _this.panelShow = true
            _this.dollar = result.routes[0].tolls
            console.log(document.getElementsByClassName('fee'))
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
    // 处理途径点
    submitForm(formName) {
      this.$message({
        message: '添加途径点成功！',
        type: 'success'
      });
      // this.$refs[formName].validate((valid) => {
      //   if (valid) {
      //     alert('submit!');
      //   } else {
      //     console.log('error submit!!');
      //     return false;
      //   }
      // });
    },

    // resetForm(formName) {
    //   this.$refs[formName].resetFields();
    // },

    // 移除途径点
    removeWayPoint(item) {
      var index = this.dynamicValidateForm.wayPoints.indexOf(item)
      if (index !== -1) {
        this.dynamicValidateForm.wayPoints.splice(index, 1)
      }
    },
    // 添加途径点
    addWayPoint() {
      this.dynamicValidateForm.wayPoints.push({
        city: '',
        detailLocation: '',
        key: Date.now()
      });
    }
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