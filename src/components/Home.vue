<template>
  <div>
    <TopHeader/>
    <router-view/>
    <FooterBottom/>
  </div>

</template>

<script>
import TopHeader from "@/components/TopHeader.vue";
import FooterBottom from "@/components/FooterBottom.vue";

export default {
  name: "Home",
  components: {
    TopHeader,
    FooterBottom,
  }
}
</script>

<style>
@import "@/assets/css/index.css";
@import "@/assets/css/base.css";
@import "@/assets/css/order.css";
</style>