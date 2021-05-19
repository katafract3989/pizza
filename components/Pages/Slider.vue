<template>
  <div class="mt-3">
    <b-carousel
      id="carousel-1"
      v-model="slide"
      :interval="2000"
      controls
      indicators
      background="#ababab"
      img-width="1024"
      img-height="480"
      @sliding-start="onSlideStart"
      @sliding-end="onSlideEnd"
    >
      <!-- Text slides with image -->
      <b-carousel-slide
        img-src="https://dodopizza-a.akamaihd.net/static/Img/Banners/g_1615063943_1a6c222c93d742e9b369396d68cd129e.jpeg"
      ></b-carousel-slide>

      <b-carousel-slide
        img-src="https://dodopizza-a.akamaihd.net/static/Img/Banners/g_1615057653_cdb8d6b6db39453997c0bc4fefeeaf5e.jpeg"
      ></b-carousel-slide>

      <b-carousel-slide
        img-src="https://dodopizza-a.akamaihd.net/static/Img/Banners/g_1611871031_fcfb6a4d00c74c4894ebc4d74e4f14e2.jpeg"
      ></b-carousel-slide>
    </b-carousel>

    <!-- <p class="mt-4">
      Slide #: {{ slide }}<br />
      Sliding: {{ sliding }}
    </p> -->
  </div>
</template>

<script>
import Vue from 'vue'
import { CarouselPlugin } from 'bootstrap-vue'
Vue.use(CarouselPlugin)
export default {
  components: {},
  data() {
    return {
      slide: 0,
      sliding: null,
    }
  },
  methods: {
    onSlideStart(slide) {
      this.sliding = true
    },
    onSlideEnd(slide) {
      this.sliding = false
    },
  },
}
</script>
