<template>
    <div class="map_wrap">
      <CurrentQuery/>
    </div>
  </template>
  <script>
  import CurrentQuery from "@/components/CurrentQuery.vue";
  export default {
    name: 'Map',
    components: {
        CurrentQuery,
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
  