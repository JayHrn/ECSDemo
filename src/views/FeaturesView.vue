<!--  -->
<template>
    <div>
        
      <div id="img_show">
        <img class="info-img" src="../assets/img/index/fea.jpg" style="width: 100%;height: 350px;">
      </div>
      <div style="background-color: aliceblue;">
        &nbsp;&nbsp;&nbsp;&nbsp;
        <h2 style="text-align:center">项目特色</h2>
        <el-divider></el-divider>
  
  
        <el-row :gutter="0" class="info_card">
          <el-col :span="10">
            <el-card shadow="never" style="margin-left: 80px;">
              <img class="info-img" src="../assets/img/index/feature.jpg" style="width: 100%; height: 100%; margin-top:80px;">
            </el-card>
          </el-col>
          <el-col :span="10">
            <el-card shadow="never" class="detail-card">
              <div class="button-forward">
                  <el-button  type="danger" >Features</el-button>
                </div>
              <div>
                
                <br>
                <p>&nbsp;&nbsp;&nbsp;&nbsp;
                    本项目从当今物流问题出发，实事求是的从理论提出到切实做技术，通过设计网站平台功能，通过平台可以使得物流减少浪费不必要的成本，拉近企业与用户的关系，团队助力从问题提出到如何解决问题，队员思想之间的碰撞，找出解决问题的方案，用技术展示出来。使该技术可以为物流服务，在之后不断地更新优化中，将其完全融入到物流中，逐步运用，体现其价值。
                </p>
                <br>
                <p>&nbsp;&nbsp;&nbsp;&nbsp;
                    快速定位查询得到最优策略，选择自己想要得到达到的目的，例如：最快捷模式、最经济模式、最短距离模式、实时路况的考虑等等。达到企业与用户共赢。
                </p>
              </div>
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
  