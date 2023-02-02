<!--  -->
<template>
    <div>
        
      <div id="img_show">
        <img class="info-img" src="../assets/img/index/production.jpg" style="width: 100%">
      </div>
      <div style="background-color: aliceblue;">
        &nbsp;&nbsp;&nbsp;&nbsp;
        <h2 style="text-align:center">产品内容</h2>
        <el-divider></el-divider>
  
  
        <el-row :gutter="0" class="info_card">
          <el-col :span="10">
            <el-card shadow="never" style="margin-left: 80px;">
              <img class="info-img" src="../assets/img/index/pro_con1.jpg" style="width: 100%; height: 100%; margin-top:100px;">
            </el-card>
          </el-col>
          <el-col :span="10">
            <el-card shadow="never" class="detail-card">
              <div class="button-forward">
                  <el-button box-shadow="0 2px 4px rgba(0, 0, 0, .12), 0 0 6px rgba(0, 0, 0, .04)" >Production</el-button>
                </div>
              <div>
                
                <br>
                <p>&nbsp;&nbsp;&nbsp;&nbsp;
                    优化配送路线技术，是针对目前电商物流所突出的问题，进行的解决方案，不光专注于为了公司损失不必要的利益，更多是为了让用户可以在当今电商的社会中，享受到更好更方便的服务，促进消费的增长。通过智能路线规划，使得可以结合大量数据，秒算排车路线，最终制定符合运输配送目标的优化配送路线，如：更短里程、更少费用、更短时间、更少车辆。通过数据采集、分析和判断得到优化后的结果。通过路线分配和车辆行驶路径进行就近匹配，尽量顺路顺点，避免多点绕路、延迟到店等现象。 避免交通堵塞等现象，确保货物定时送达，货到人手。

                </p>
                <br>
                
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
  