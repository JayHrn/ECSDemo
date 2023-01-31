<template>
    <div class="map_wrap">
      <ExchangeMap/>
    </div>
  </template>
  
  <script>
  import ExchangeMap from "@/components/ExchangeMap.vue";
  
  export default {
    name: "ExchangeView",
    components: {
        ExchangeMap
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