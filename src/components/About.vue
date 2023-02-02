<template>
  <!-- about us -->
  <div class="advantage-wrapper">
    <div class="advantage-content">
      <div class="advantage-title">
        <h2 id="关于十漓">关于十漓</h2>
        <p>运输极速，价格实惠，在邮局、海关和航空公司都拥有优先权。</p>
      </div>
      <div class="advantage-detail">
        <div class="advantage">
          <i class="iconfont iconhuiju"></i>
          <router-link to="/about/teamProduce"><h3>团队简介</h3></router-link>
          <!--          <p>服务范围涵盖美国、加拿大、墨西哥和欧洲等多地</p>-->
        </div>
        <div class="advantage">
          <i class="iconfont iconcaidan"></i>

          <router-link to="/about/productionCon"><h3>产品内容</h3></router-link>
        </div>
        <div class="advantage">
          <i class="iconfont iconhuojian"></i>

          <router-link to="/about/features"><h3>项目特色</h3></router-link>
        </div>
        <div class="advantage">
          <i class="iconfont iconshizhong"></i>
          <router-link to="/about/technology"><h3>项目技术</h3></router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "About"
}
</script>

<style>

</style>