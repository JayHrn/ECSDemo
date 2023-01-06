<template>
  <div class="home">
    <Carousel/>
    <Business/>
    <About/>
    <News/>
  </div>
</template>

<script>
import Carousel from "@/components/Carousel.vue";
import Business from "@/components/Business.vue";
import About from "@/components/About.vue";
import News from "@/components/News.vue";

export default {
  name: 'HomeView',
  components: {
    Carousel,
    Business,
    About,
    News,
  }
}
</script>
