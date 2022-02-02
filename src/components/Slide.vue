<template>
  <div class="carousel-wrapper">
    <div class="slide-image">
      <img
        v-if="imageNumber === 0"
        class="image"
        src="../assets/atmosphere.png"
      />
      <img v-if="imageNumber === 1" class="image" src="../assets/monk.png" />

      <img
        v-if="imageNumber === 2"
        class="image"
        src="../assets/raised-eyebrow.png"
      />
      <img v-if="imageNumber === 3" class="image" src="../assets/heart.png" />
    </div>
    <div class="slide-content">
      <!-- <h2 v-if="showDefaultView === true" class="slide-title">
        What's the air like?
      </h2> -->
      <h2 class="slide-title">Air Quality: {{ aqiLevelDisplay }}</h2>
      <p class="slide-subdeck">
        You can search for the current air quality levels for any city across
        the world or simply check your current location. Geolocation must be
        'allowed' on your device.
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "CarouselSlide",
  props: ["aqi"],
  data() {
    return {
      imageNumber: 0,
      showDefaultView: true,
    };
  },
  computed: {
    aqiLevelDisplay() {
      if (this.aqi === 1) {
        this.showDefaultView = !this.showDefaultView;
        this.imageNumber = 1;
        return "Good";
      } else if (this.aqi === 2) {
        this.showDefaultView = !this.showDefaultView;
        this.imageNumber = 1;
        return "Fair";
      } else if (this.aqi === 3) {
        this.showDefaultView = !this.showDefaultView;
        this.imageNumber = 2;
        return "Moderate";
      } else if (this.aqi === 4) {
        this.showDefaultView = !this.showDefaultView;
        this.imageNumber = 3;
        return "Poor";
      } else if (this.aqi === 5) {
        this.showDefaultView = !this.showDefaultView;
        this.imageNumber = 3;
        return "Very Poor";
      }
    },
  },
  methods: {},
};
</script>

<style>
.carousel-wrapper {
  display: flex;
  flex-direction: column;
}
.slide-image {
  text-align: center;
}
.image {
  width: 80%;
}
.slide-content {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.slide-subdeck {
  padding: 10px 10%;
  font-size: 0.8rem;
}
</style>
