<template>
  <div class="map_wrap">
    <DeliveryMap/>
  </div>
</template>

<script>
import DeliveryMap from "@/components/DeliveryMap.vue";

export default {
  name: "DeliveryView",
  components: {
    DeliveryMap
  }
}
</script>

<style scoped>
.map_wrap{
  width: 1200px;
  max-width: 1200px;
  height: calc(600px + 1.5rem);
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  margin: auto;
  margin-top: 30px;
  margin-bottom: 30px;
}
</style>