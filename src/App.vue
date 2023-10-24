<template>
  <div>
    <Carousel :autoplay="true" :loop="true">
      <Slide v-for="image in images" :key="image.id">
        <img :src="image.download_url" :alt="image.author" style="width: 100%; height: 100%;">
      </Slide>
    </Carousel>
  </div>
</template>

<script>
import Carousel from "./components/ImageCarousel.vue";
import Slide from "./components/SlideItem.vue";

export default {
  components: { Carousel, Slide },
  data() {
    return {
      images: [],
    };
  },
  created() {
    this.fetchImages();
  },
  methods: {
    async fetchImages() {
      try {
        const response = await fetch('https://picsum.photos/v2/list');
        const data = await response.json();
        this.images = data;
      } catch (error) {
        console.error('Error fetching images: ', error);
      }
    },
  },
};

</script>

<style>

</style>