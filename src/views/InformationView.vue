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
                <el-button type="primary">前往查看</el-button>
              </div>
            </div>
          </el-card>
        </el-col>
      </el-row>

      <el-row :gutter="0" class="info_card">

        <el-col :span="10">
          <el-card shadow="never" class="detail-card">

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
              <el-button type="primary">前往查看</el-button>
            </div>


          </el-card>
        </el-col>
        <el-col :span="10">
          <el-card shadow="never" style="margin-left: 80px;">
            <img class="info-img" src="../assets/img/index/info_con1.jpg">
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
  padding: 40px;
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
