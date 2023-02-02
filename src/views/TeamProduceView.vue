<template>
  <div>
    <div id="img_show">
      <img class="info-img" src="../assets/img/index/team.jpg" style="height: 300px;">
    </div>
    <div style="background-color: aliceblue;">
      &nbsp;&nbsp;&nbsp;&nbsp;
      <h2 style="text-align:center">组织结构建设</h2>
      <el-divider></el-divider>
      <el-row :gutter="0" class="info_card">

        <el-col :span="20">
          <el-card shadow="never" class="detail-card">
            <div>
              <br>
              <p>
                团队建立初期，各成员各有所长，实现了不同专业的结合。为了提高工作效率，对每个成员进行合理、科学的分配，各成员之间协调配合，各个环节之间紧密衔接，共同完成策划书、网站以及PPT演讲。从物流问题上来讲，我们专注于优化物流配送技术，致力于解决当前物流费用高，耗时长等问题，是配送安排合理化，有利于提高企业效率和竞争力。
              </p>
              <br>
              <el-row :gutter="0" class="info_card">
                <el-col :span="10">
                  <el-card shadow="never" style="height: 80%;">
                    <img class="info-img" src="../assets/img/index/info_con3.jpg" style="width: 100%;height: 100%;">
                  </el-card>
                </el-col>
                <el-col :span="10">
                  <el-card shadow="never" class="detail-card">
                    <div>
                      <h2 style="color: cadetblue; font-family: 楷体;">数据分析小组</h2>
                      <br>
                      <p>
                        负责对近年来的物流相关的信息和数据进行收集、梳理、统计、对比、分析以及汇总
                      </p>
                      <div class="button-forward">
                        <el-button type="primary"> DataAnalysis</el-button>
                      </div>
                    </div>
                  </el-card>
                </el-col>
              </el-row>

              <el-row :gutter="0" class="info_card">

                <el-col :span="10">
                  <el-card shadow="never" class="detail-card">
                    <div>
                      <h2 style="color: cornflowerblue; font-family: 楷体;">策划小组</h2>
                      <br>
                      <p>
                        负责制定项目计划与方案
                      </p>
                      <div class="button-forward">
                        <el-button style="background-color: #303133"><p style="color: white;">PlanningTeam</p>
                        </el-button>
                      </div>
                    </div>
                  </el-card>
                </el-col>
                <el-col :span="10">
                  <el-card shadow="never" style="height: 80%;">
                    <img class="info-img" src="../assets/img/index/info_con4.jpg" style="width: 100%;height: 100%;">
                  </el-card>
                </el-col>
              </el-row>

              <el-row :gutter="0" class="info_card">
                <el-col :span="10">
                  <el-card shadow="never" style="height: 80%;">
                    <img class="info-img" src="../assets/img/index/info_con5.jpg" style="width: 100%;height: 100%;">
                  </el-card>
                </el-col>
                <el-col :span="10">
                  <el-card shadow="never" class="detail-card">
                    <div>
                      <h2 style="color: darkslateblue; font-family: 楷体;">技术小组</h2>
                      <br>
                      <p>
                        负责对平台网站的建设，提供一定的技术支持
                      </p>
                      <div class="button-forward">
                        <el-button type="danger"> Technology</el-button>
                      </div>
                    </div>
                  </el-card>
                </el-col>
              </el-row>

              <el-row :gutter="0" class="info_card">

                <el-col :span="10">
                  <el-card shadow="never" class="detail-card">
                    <div>
                      <h2 style="color: cornflowerblue; font-family: 楷体;">设计与新媒体小组</h2>
                      <br>
                      <p>
                        负责网站的页面设计与配色，制作PPT以及演讲
                      </p>
                      <div class="button-forward">
                        <el-button style="background-color:lightyellow"><p style="color: black;">PlanningTeam</p>
                        </el-button>
                      </div>
                    </div>
                  </el-card>
                </el-col>
                <el-col :span="10">
                  <el-card shadow="never" style="height: 80%;">
                    <img class="info-img" src="../assets/img/index/info_con3.jpg" style="width: 100%;height: 100%;">
                  </el-card>
                </el-col>
              </el-row>
            </div>
          </el-card>
        </el-col>
      </el-row>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TeamProduceView',
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

.button-forward {
  margin-top: 15px;
}

</style>

