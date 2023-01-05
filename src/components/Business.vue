<template>
  <!-- business -->
  <div class="business-wrapper">
    <div class="business-content">
      <div class="business-title">
        <h2 id="businessTitleWuliu" class="active"><a href="javascript:void(0);" @click="change">物流业务</a></h2>
        <h2 id="businessTitleDianshang"><a href="javascript:void(0);" @click="change">电商业务</a></h2>
      </div>
      <div id="businessWuliu" class="business-detail business-checked">
        <div class="business-introduce">国内业务</div>
        <div class="business-list-wrapper">
          <div class="business-list">
            <img src="../assets/img/index/business_icon1_1.jpg">
            <div>
              <h3>隐私面单</h3>
              <p>个人信息，专业保护</p>
            </div>
          </div>
          <div class="business-list">
            <img src="../assets/img/index/business_icon1_2.jpg">
            <div>
              <h3>优先送</h3>
              <p>中转派送，为您优先</p>
            </div>
          </div>
          <div class="business-list">
            <img src="../assets/img/index/business_icon1_3.jpg">
            <div>
              <h3>云打印</h3>
              <p>轻松下单，极速打印</p>
            </div>
          </div>
          <div class="business-list">
            <img src="../assets/img/index/business_icon1_6.jpg">
            <div>
              <h3>电子面单</h3>
              <p>打印结算，高效精准</p>
            </div>
          </div>
          <div class="business-list">
            <img src="../assets/img/index/business_icon1_4.jpg">
            <div>
              <h3>货到付款</h3>
              <p>闪电付款，周期灵活</p>
            </div>
          </div>
          <div class="business-list">
            <img src="../assets/img/index/business_icon1_5.jpg">
            <div>
              <h3>保价</h3>
              <p>打印结算，高效精准</p>
            </div>
          </div>
        </div>
      </div>
      <div id="businessDianshang" class="business-detail">
        <div class="business-introduce">电商业务</div>
        <div class="business-list-wrapper">
          <div class="business-list">
            <img src="../assets/img/index/business_icon4_1.jpg">
            <div>
              <h3>全新创客模式</h3>
              <p>创客分享消费获取佣金</p>
            </div>
          </div>
          <div class="business-list">
            <img src="../assets/img/index/business_icon4_2.jpg">
            <div>
              <h3>配送一体化</h3>
              <p>依托快递行业高覆盖，配送高效</p>
            </div>
          </div>
          <div class="business-list">
            <img src="../assets/img/index/business_icon4_3.jpg">
            <div>
              <h3>商品时效</h3>
              <p>原产地商家合作，确保新鲜、绿色、优质</p>
            </div>
          </div>
          <div class="business-list">
            <img src="../assets/img/index/business_icon4_4.jpg">
            <div>
              <h3>推广强度</h3>
              <p>多渠道，精准定向，辐射范围广</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Business",
  methods:{
    change(){
      let twl = document.getElementById("businessTitleWuliu");
      let tds = document.getElementById("businessTitleDianshang");
      let wl = document.getElementById("businessWuliu");
      let ds = document.getElementById("businessDianshang");
      twl.onclick = function () {
        twl.classList.add("active");
        tds.classList.remove("active");
        wl.classList.add("business-checked");
        ds.classList.remove("business-checked");
      };
      tds.onclick = function () {
        tds.classList.add("active");
        twl.classList.remove("active");
        ds.classList.add("business-checked");
        wl.classList.remove("business-checked");
      }
    }
  }
}
</script>

<style scoped>

</style>