<template>
  <div class="carousel-wrapper">
    <div class="slide-image">
      <img
        v-if="imageNumber === 0"
        class="image"
        src="../assets/atmosphere.png"
      />
      <img
        v-else-if="imageNumber === 1"
        class="image"
        src="../assets/monk.png"
      />

      <img
        v-else-if="imageNumber === 2"
        class="image"
        src="../assets/like.png"
      />
      <img
        v-else-if="imageNumber === 3"
        class="image"
        src="../assets/raised-eyebrow.png"
      />
      <img
        v-else-if="imageNumber === 4"
        class="image"
        src="../assets/concern.png"
      />
      <img
        v-else-if="imageNumber === 5"
        class="image"
        src="../assets/heart.png"
      />
    </div>

    <div  class="slide-content">
      <div class="slide-title">
        <h2 v-if="showPollutantInfo" >Air Quality:</h2>
        <h2 >{{ aqiLevelDisplay }}</h2>
      </div>

      
      <p  class="results">
        <ul v-if="showPollutantInfo" class="results-grid">
          <li class="results-list-item" v-for="(level, pollutant) in pollutants" :key="level">
             <span class="pollutant-name">{{pollutant.toUpperCase()}}</span> : <span class="pollutant-level">{{level}}</span>
          </li>
        </ul>
      </p>
    </div>
    <div  class="slide-content">
      <div class="slide-title">
        <h2 v-if="!showPollutantInfo" >What's the air like?</h2>
      </div>

      <p v-if="!showPollutantInfo" class="results">
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
  props: ["aqi", "pollutants"],
  data() {
    return {
      imageNumber: 0,

      showPollutantInfo: false,
    };
  },
// beforeMount(){
//   this.imageNumber = 0;
//   this.showPollutantInfo = false;
// },
  computed: {
    aqiLevelDisplay() {
      if (this.aqi === 1) {
        this.showPollutantInfo = true;
        this.imageNumber = 1;
        return "Good";
      } else if (this.aqi === 2) {
        this.showPollutantInfo = true;
        this.imageNumber = 2;
        return "Fair";
      } else if (this.aqi === 3) {
        this.showPollutantInfo = true;
        this.imageNumber = 3;
        return "Moderate";
      } else if (this.aqi === 4) {
        this.showPollutantInfo = true;
        this.imageNumber = 4;
        return "Poor";
      } else if (this.aqi === 5) {
        this.showPollutantInfo = true;
        this.imageNumber = 5;
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
  justify-content: space-evenly;
  height: 100%;
}
.slide-image {
  text-align: center;
}
.image {
  width: 60%;
}
.slide-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  
}
.slide-title {
  /* width: 100%; */
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  margin-bottom: 10px;
}
.slide-title h2 {
  margin: 0 10px;
}
.results {
  width: 70%;
  /* padding: 10px 10%; */
  font-size: 0.8rem;
  line-height: 1.2;
}
.results-grid {
  list-style: none;
  padding: 0;
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 0.5rem;
}
.results-list-item {
  justify-self: center;
}
.pollutant-name {
  font-weight: bolder;
  color: rgb(4, 154, 255)
}
.pollutant-level {
  font-weight: bolder;
}
</style>
