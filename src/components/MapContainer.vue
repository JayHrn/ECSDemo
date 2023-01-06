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
            <el-select v-model="drivePolicy" clearable placeholder="请选择驾车策略">
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
          <el-button size="medium" @click="driver" type="primary">查找</el-button>
        </div>

      </div>
    </div>

    <div class="map">
      <div id="MapContainer">
      </div>
      <div id="panel" v-show="panelShow">
        <div class="fee">路费：{{ this.dollar }}元</div>
      </div>
    </div>
    <!--    添加途径点-->
    <!--    <el-dialog-->
    <!--        title="添加途径点"-->
    <!--        :visible.sync="wayPointsDialogVisible"-->
    <!--        width="50%"-->
    <!--        center>-->

    <!--      <el-form :model="dynamicValidateForm" ref="dynamicValidateForm" label-width="100px" class="demo-dynamic">-->
    <!--        <el-form-item-->
    <!--            v-for="(domain, index) in dynamicValidateForm.domains"-->
    <!--            :label="'途径点' + (index+1)"-->
    <!--            :key="domain.key"-->
    <!--            :prop="'domains.' + index + '.value'"-->
    <!--            :rules="{required: true, message: '途径点信息不能为空', trigger: 'blur'}"-->
    <!--        >-->
    <!--          <el-cascader-->
    <!--              size="large"-->
    <!--              :options="options"-->
    <!--              v-model="selectedOptions"-->
    <!--              placeholder="请选择省市区"-->
    <!--              @change="handleChange">-->
    <!--          </el-cascader>-->
    <!--          <el-input-->
    <!--              v-model="destination"-->
    <!--              placeholder="请输入详细地址"-->
    <!--              clearable>-->
    <!--          </el-input>-->
    <!--          &lt;!&ndash;          <el-input v-model="domain.value"></el-input>&ndash;&gt;-->
    <!--          <el-button @click.prevent="removeDomain(domain)">删除</el-button>-->
    <!--        </el-form-item>-->

    <!--        <el-form-item>-->

    <!--          <el-button @click="addDomain">新增途径点</el-button>-->
    <!--          <el-button @click="wayPointsDialogVisible = false">取 消</el-button>-->
    <!--          <el-button type="primary" @click="submitForm('dynamicValidateForm'), wayPointsDialogVisible = false ">提交-->
    <!--          </el-button>-->

    <!--          &lt;!&ndash;          <el-button @click="resetForm('dynamicValidateForm')">重置</el-button>&ndash;&gt;-->
    <!--        </el-form-item>-->
    <!--      </el-form>-->

    <!--      &lt;!&ndash;      <span slot="footer" class="dialog-footer">&ndash;&gt;-->
    <!--      &lt;!&ndash;        <el-button @click="wayPointsDialogVisible = false">取 消</el-button>&ndash;&gt;-->
    <!--      &lt;!&ndash;        <el-button type="primary" @click="wayPointsDialogVisible = false">确 定</el-button>&ndash;&gt;-->
    <!--      &lt;!&ndash;      </span>&ndash;&gt;-->
    <!--    </el-dialog>-->
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
      map: null,
      panelShow: false,
      dollar: '',
      // 起始地城市
      startCity: [],
      // 起始地具体位置
      startDetail: '',

      // 起始地城市
      destinationCity: [],
      // 起始地具体位置
      destinationDetail: '',

      // 驾车策略
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
      drivePolicy: '',


      start: '',
      destination: '',
      waypoints: [
        {keyword: '天津站', city: '天津'}
      ],
      // 省市区
      options: regionData,
      selectedOptions: [],
      // 途径点对话框
      wayPointsDialogVisible: false,

      dynamicValidateForm: {
        domains: [{
          value: ''
        }],
        email: ''
      }
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
      console.log(this.drivePolicy)
      let _this = this; //便于获取vue对象
      let drivingOptions = {
        /* 驾车路线规划策略
         * AMap.DrivingPolicy.LEAST_TIME  //最快捷模式
         * AMap.DrivingPolicy.LEAST_FEE   //最经济模式
         * AMap.DrivingPolicy.LEAST_DISTANCE  //最短距离模式
         * AMap.DrivingPolicy.REAL_TRAFFIC  //考虑实时路况
         */
        policy: this.drivePolicy,
        panel: 'panel',
        map: this.map,
      };
      let driving = new AMap.Driving(drivingOptions)
      console.log(driving)
      console.log(CodeToText[this.destinationCity[0]] + CodeToText[this.destinationCity[1]] + CodeToText[this.destinationCity[2]])
      let points = [
        {
          keyword: this.startDetail,
          city: CodeToText[this.startCity[0]] + CodeToText[this.startCity[1]] + CodeToText[this.startCity[2]]
        },
        // {keyword: '天津站', city: '天津'},
        {
          keyword: this.destinationDetail,
          city: CodeToText[this.destinationCity[0]] + CodeToText[this.destinationCity[1]] + CodeToText[this.destinationCity[2]]
        },
      ]
      // let startPoint = {keyword: this.start, city: this.start}
      // let destinationPoint = {keyword: this.destination, city: this.destination}
      // points.push(startPoint, destinationPoint)

      driving.search(points, function (status, result) {
        _this.panelShow = true
        console.log(result)
        // console.log("路费：" + result.routes[0].tolls)
        // console.log("收费路段长度：" + result.routes[0].tolls_distance)
        // console.log(result)
        _this.dollar = result.routes[0].tolls
        // // let steps=result.steps;
        // // console.log(steps);
        // console.log(result.waypoints)
      })
    },

    selectedStartCity(location) {
      console.log("起始地城市为：" + CodeToText[location[1]])
    }
    ,
    selectedDestinationCity(location) {
      console.log("目的地城市为：" + CodeToText[location[1]])
    }
    ,
    // 处理途径点
    submitForm(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          alert('submit!');
        } else {
          console.log('error submit!!');
          return false;
        }
      });
    }
    ,
    resetForm(formName) {
      this.$refs[formName].resetFields();
    }
    ,
    removeDomain(item) {
      var index = this.dynamicValidateForm.domains.indexOf(item)
      if (index !== -1) {
        this.dynamicValidateForm.domains.splice(index, 1)
      }
    }
    ,
    addDomain() {
      this.dynamicValidateForm.domains.push({
        value: '',
        key: Date.now()
      });
    }
  },
}
</script>

<style scoped>
@import "@/assets/css/map.css";

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

.input-line {
  display: flex;
}

.input-area {
  margin: auto;
}

.input-title {
  line-height: 40px;
  /*margin-right: 8px;*/
  width: 80px;
  text-align: right;
}

.el-cascader.el-cascader--large, .el-input.el-input--suffix {
  padding: 8px;
}

button.el-button.el-button--primary.el-button--medium {
  float: left;
  margin: 10px 70px;
}

/deep/ .el-select > .el-input {
  padding: 8px;
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

#panel {
  position: absolute;
  width: calc(250px + 1rem);
  height: calc(600px + 1.5rem);
  top: 100px;
  border-radius: 8px;
  display: flex;
  overflow: auto;
  flex-wrap: wrap;
}

/*前往百度地图消失*/
/deep/ .amap-call {
  display: none !important;
}

/deep/ dl.plan.plan-nobus {
  background: rgba(255, 255, 255);
}

/deep/ .fee {
  background-color: #ffffff;
  color: #565656;
  width: 100%;
  font-size: 14px;
  border: 1px solid silver;
  text-align: center;
  border-radius: 8px 0 0 0;
  font-weight: bold;
}


/* 表单区域 */
/deep/ .el-form-item__content {
  display: flex;
  align-items: center;
}


</style>