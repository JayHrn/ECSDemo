<!--  -->
<template>
    <div>
        
      <div id="img_show">
        <img class="info-img" src="../assets/img/index/feature.jpg" style="width: 100%;height: 400px;">
      </div>
      <div style="background-color: aliceblue;">
        &nbsp;&nbsp;&nbsp;&nbsp;
        <h1 style="text-align:center">项目技术</h1>
        <el-divider></el-divider>
  
  
        <el-row :gutter="0" class="info_card">
          <el-col :span="10">
            <el-card shadow="never" style="margin-left: 80px;">
              <img class="info-img" src="../assets/img/index/technology1.jpg" style="width: 100%; height: 100%; margin-top:80px;">
            </el-card>
          </el-col>
          <el-col :span="10">
            <el-card shadow="never" class="detail-card" style="margin-top: 80px;" >
             
              <div>
                <h3 style="font-family: 楷体 ; color: darkslateblue;">项目技术路线</h3>
                <br>
                <p style="color: dimgrey;">&nbsp;&nbsp;&nbsp;&nbsp;
                    本项目从当今物流问题出发，实事求是的从理论提出到切实做技术，通过设计网站平台功能，通过平台可以使得物流减少浪费不必要的成本，拉近企业与用户的关系，团队助力从问题提出到如何解决问题，队员思想之间的碰撞，找出解决问题的方案，用技术展示出来。使该技术可以为物流服务，在之后不断地更新优化中，将其完全融入到物流中，逐步运用，体现其价值。
                </p>
                
              </div>
            </el-card>
          </el-col>
        </el-row>
  
        <el-row :gutter="0" class="info_card">

            <el-col :span="10">
            <el-card shadow="never" class="detail-card">
              
              <div>
                <h3 style="font-family: 楷体 ; color: darkslateblue;">技术设计</h3>
                <br>
                <p style="color: dimgrey;">&nbsp;&nbsp;&nbsp;&nbsp;
                    将时间、成本、资源、效率、环境约束集中整合优化，实现现代物流管理低成本高效率，是物流运营计划与实际运营之间的有效结合的关键。运输网络四通八达，通过货车将包裹配送到各配送站，而配送管理部门通过对全国路线及实时路况的掌握，为配送部门的快递小哥提前规划好最优化的路径。通过对配载线路技术的优化，可以大大提高配送的效率。在配送业务中，配路线优化技术对配送企业提高服务质量、降低物流成本、增加经济效益有着绝对性的影响。
                </p>
                <br>
                <p style="color: dimgrey;">&nbsp;&nbsp;&nbsp;&nbsp;
                    通过智能路线优化，结合大量数据，秒算排车路线，最终制定符合运输配送目标的优化配送路线。最经济模式、最快捷模式、最短距离模式、实时路况考虑等选择的运用使得可以方便快递员快速配送，节省时间路程成本。
                </p>
              </div>
            </el-card>
          </el-col>
          <el-col :span="10">
            <el-card shadow="never" style="margin-left: 80px;">
              <img class="info-img" src="../assets/img/index/technology2.jpg" style="width: 100%; height: 100%; margin-top:80px;">
            </el-card>
          </el-col>
          
        </el-row>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'InformationView',
    data() {
      return {
        imgs: [
          {
            id: 1, img: require('../assets/img/index/info1.jpg')
          },
          {
            id: 2, img: require('../assets/img/index/info2.jpg')
          },
          {
            id: 3, img: require('../assets/img/index/info3.jpg')
          },
          {
            id: 4, img: require('../assets/img/index/info4.jpg')
          }
        ]
      }
    }
  }
  </script>
  
  <style scoped>
  .img_show {
    background-color: dimgrey;
    padding-top: 50px;
    width: 100%;
  }
  
  img {
    align-content: center;
  }
  
  .el-card {
    border: none;
  }
  
  .el-col-10 {
    height: 440px;
  }
  
  .detail-card {
    padding: 30px;
  }
  
  h3 {
    font-size: 26px;
    text-underline: #f5a546;
  }
  
  p {
    font-size: 16px;
  }
  
  .info_card {
    display: flex;
    align-items: center;
    flex-wrap: nowrap;
    justify-content: center;
  }
  .button-forward{
    margin-top: 15px;
  }
  
  </style>
  