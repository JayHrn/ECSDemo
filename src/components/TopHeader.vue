<template>
  <!-- header -->
  <div>
    <header class="nav-wrapper">
      <div class="nav-content">
        <!-- logo格式 -->
        <div class="nc-logo">
          <img src="../assets/img/logo-name.png">
        </div>
        <!-- 菜单 -->
        <div class="nc-menu">
          <ul>
            <li class="active">
              <router-link to="/">首页</router-link>
<!--              <a href="../官网/index.html">首页</a>-->
            </li>

            <!-- 客户服务子菜单 -->
            <li>
              <a href="./pages/order/orderonline.html">在线下单</a>
              <div class="nc-menulist">
                <div class="nc-menulist-li">
                  <a href="javascript:void(0);">单号查询</a>
                  <a href="javascript:void(0);">网点查询</a>
                  <a href="javascript:void(0);">价格时效查询</a>
                </div>
              </div>
            </li>

            <!-- 业务介绍子菜单 -->
            <li><a href="javascript:void(0);">业务介绍</a>
              <div class="nc-menulist">
                <div class="nc-menulist-li">
                  <h4>快递</h4>
                  <router-link to="/map">特准快递</router-link>
<!--                  <a href="javascript:void(0);">特准快递</a>-->
                  <a href="javascript:void(0);">电商尊享</a>
                  <a href="javascript:void(0);">标准快递</a>
                  <a href="javascript:void(0);">大件快递</a>
                </div>
                <div class="nc-menulist-li">
                  <h4>零担</h4>
                  <a href="javascript:void(0);">精准汽运</a>
                  <a href="javascript:void(0);">精准空运</a>
                  <a href="javascript:void(0);">精准卡航</a>
                </div>
                <div class="nc-menulist-li">
                  <h4>仓储</h4>
                  <a href="javascript:void(0);">仓配一体化</a>
                  <a href="javascript:void(0);">同城仓配</a>
                </div>
              </div>
            </li>

            <!-- 帮助中心子菜单 -->
            <li><a href="javascript:void(0);">帮助中心</a></li>

            <!-- 关于我们子菜单 -->
            <li><a href="javascript:void(0);">关于七步</a></li>
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
export default {
  name: "TopHeader"
}
</script>

<style scoped>

</style>