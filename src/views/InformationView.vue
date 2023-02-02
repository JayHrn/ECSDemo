<template>
  <div>
    <div id="img_show">
      <el-carousel :interval="4000" arrow="always" height="500px">
        <el-carousel-item v-for="item in imgs" :key="item.id">
          <img :src="item.img" class="image" width="100%" height="100%">
        </el-carousel-item>
      </el-carousel>
    </div>
    <div>
      &nbsp;&nbsp;&nbsp;&nbsp;
      <h2 style="text-align:center">公司信息</h2>
      <el-divider></el-divider>


      <el-row :gutter="0" class="info_card">
        <el-col :span="10">
          <el-card shadow="never" style="margin-left: 80px;">
            <img class="info-img" src="../assets/img/index/info_con1.jpg">
          </el-card>
        </el-col>
        <el-col :span="10">
          <el-card shadow="never" class="detail-card">
            <div>
              <h3>中国邮政</h3>
              <br>
              <p>
                EMS拥有首屈一指的航空和陆路运输网络以及200多个高效发达的邮件处理中心，国内范围通达全覆盖，并拥有多种不同的快递产品和增值服务，满足客户多样化、个性化的寄件需求。
              </p>
              <br>
              <p>
                中国邮政国际业务为用户提供通达全球200多个国家和地区的寄递服务。根据不同产品，可提供信息查询、邮件保价、延误赔偿和丢失赔偿等增值服务，以满足用户寄递物品、文件资料和信件等不同类型的需求。
              </p>
              <div class="button-forward">
                <el-button type="primary"><a href="https://www.ems.com.cn/" target="_blank">前往查看</a></el-button>
              </div>
            </div>
          </el-card>
        </el-col>
      </el-row>

      <el-row :gutter="0" class="info_card">

        <el-col :span="10">
          <el-card shadow="never" class="detail-card" style="margin-left:40px;">

            <h3>圆通速运</h3>
            <br>
            <p>
              圆通速递有限公司（以下简称圆通速递）创立于2000年5月28日，目前已发展成为一家集快递物流、科技、航空、金融、商贸等为一体的综合物流服务运营商和供应链集成商。
            </p>
            <br>
            <p>
              圆通速递始终坚持“客户要求，圆通使命”的宗旨，以人为本，以客户体验为中心，以“安全、快速、便捷、可靠”为追求，着力打造品质圆通、科技圆通、绿色圆通、德善圆通，构建圆通供应链网络生态命运共同体。
            </p>
            <div class="button-forward">
              <el-button type="primary"><a href="https://www.yto.net.cn/about/intro/enterpriseoverview.html/" target="_blank">前往查看</a></el-button>
            </div>


          </el-card>
        </el-col>
        <el-col :span="10">
          <el-card shadow="never" style="margin-left: 80px;height: 80%;">
            <video src="../assets/img/index/info_convideo.mp4" autoplay="autoplay" loop="loop" style="width: 100%;height: 100%;
    -o-object-fit: cover;
    object-fit: cover;"></video>
          </el-card>
        </el-col>
      </el-row>

      <el-row :gutter="0" class="info_card">
        <el-col :span="10">
          <el-card shadow="never" style="margin-left: 80px;height: 80%;">
            <img class="info-img" src="../assets/img/index/info_con3.jpg" style="width: 100%;height: 100%;">
          </el-card>
        </el-col>
        <el-col :span="10">
          <el-card shadow="never" class="detail-card">
            <div>
              <h3>顺丰速运</h3>
              <br>
              <p>
                1993年，顺丰（股票代码：002352）诞生于广东顺德。经过多年发展，已成为国内领先的快递物流综合服务商、全球第四大快递公司。顺丰秉承“以用户为中心，以需求为导向，以体验为根本”的产品设计思维，聚焦行业特性，从客户应用场景出发，深挖不同场景下客户端到端全流程接触点需求及其他个性化需求，设计适合客户的产品服务及解决方案，持续优化产品体系与服务质量。同时，顺丰利用科技赋能产品创新，形成行业解决方案，为客户提供涵盖多行业、多场景、智能化、一体化的智慧供应链解决方案。

                </p>
              <div class="button-forward">
                <el-button type="primary"><a href="https://www.sf-express.com/chn/sc/about/company" target="_blank">前往查看</a></el-button>
              </div>
            </div>
          </el-card>
        </el-col>
      </el-row>

      <el-row :gutter="0" class="info_card">

        <el-col :span="10">
          <el-card shadow="never" class="detail-card" style="margin-left:40px;">

            <h3>申通快递</h3>
            <br>
            <p>
              申通快递品牌初创于1993年，公司致力于民族品牌的建设和发展，不断完善终端网络、中转运输网络和信息网络三网一体的立体运行体系，立足传统快递业务，全面进入电子商务领域，以专业的服务和严格的质量管理推动中国快递行业的发展。
            </p>
            <div class="button-forward">
              <el-button type="primary"><a href="https://www.sto.cn/Home/AboutUs" target="_blank">前往查看</a></el-button>
            </div>


          </el-card>
        </el-col>
        <el-col :span="10">
          <el-card shadow="never" style="margin-left: 80px;height: 80%;">
            <img class="info-img" src="https://www.sto.cn/static/img/home_news_bg.png" style="width: 100%;height: 100%;">
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
