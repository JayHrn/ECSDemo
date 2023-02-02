<template>
  <!-- header -->
  <div>
    <header class="nav-wrapper">
      <div class="nav-content">
        <!-- logo格式 -->
        <div class="nc-logo">
          <img src="../assets/img/logo-removebg-preview.png">
        </div>
        <!-- 菜单 -->
        <div class="nc-menu">
          <ul>
            <li >
              <router-link to="/">首页</router-link>
            </li>
            <!-- 客户服务子菜单 -->
<!--            <li>-->
<!--              <a href="./pages/order/orderonline.html">在线下单</a>-->
<!--              <div class="nc-menulist">-->
<!--                <div class="nc-menulist-li">-->
<!--                  <a href="javascript:void(0);">单号查询</a>-->
<!--                  <a href="javascript:void(0);">网点查询</a>-->
<!--                  <a href="javascript:void(0);">价格时效查询</a>-->
<!--                </div>-->
<!--              </div>-->
<!--            </li>-->

            <!-- 业务介绍子菜单 -->
            <li>
              <a href="javascript:void(0);">业务中心</a>
              <div class="nc-menulist">
                <div class="nc-menulist-li">
                  <h4>快递</h4>
                  <router-link to="/business/map">路线规划</router-link>
                  <router-link to="/business/location">位置查询</router-link>
                  <router-link to="/business/expressContact">快递联系</router-link>
<!--                  <a href="javascript:void(0);">交通查询</a>-->
                </div>
                <div class="nc-menulist-li">
                  <h4>服务</h4>
                  <router-link to="/business/delivery">优先派送</router-link>
                  <router-link to="/business/exchange">退换更改</router-link>
                  <router-link to="/business/quick/">加急服务</router-link>
                </div>
                <div class="nc-menulist-li">
                  <h4>信息</h4>
                  
                  <router-link to="/business/currentQuery">实时查询</router-link>
                  <router-link to="/business/information">公司信息</router-link>
                </div>
              </div>
            </li>

            <!-- 帮助中心子菜单 -->
            <li><a href="javascript:void(0);">帮助中心</a></li>

            <!-- 关于我们子菜单 -->
            <a href="/#关于十漓" id="123">关于十漓</a>

          </ul>
        </div>
        <!-- 导航右侧 -->
        <div class="nc-login">
          <a href="javascript:void(0);">登录</a>
          <a href="javascript:void(0);">注册</a>
          <a href="javascript:void(0);">简</a>
        </div>
        <!-- 搜索框
            <div class="nbc-search rf">
                <input><span>a</span>
            </div>-->
      </div>
    </header>
  </div>

</template>

<script>
import router from '@/router';
import { RouterLink } from 'vue-router';

export default {
    name: "TopHeader",
    components: { RouterLink, router }
}
</script>

<style>

</style>