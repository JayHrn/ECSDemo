<template>
  <div class="map_wrap">
    <MapContainer/>
  </div>
</template>
<script>
import MapContainer from "@/components/MapContainer.vue";
export default {
  name: 'Map',
  components: {
    MapContainer,
  }
}
</script>
<style>
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
