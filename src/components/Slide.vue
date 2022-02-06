<template>
  <div class="carousel-wrapper">
    <template v-if="defaultView === true">
      <div class="slide-image">
        <img class="image" src="../assets/atmosphere.png" alt="" />
      </div>
      <div class="slide-content">
        <h2>What's the air like?</h2>
        <p class="results">
          You can search for the current air quality levels for any city across
          the world or simply check your current location. Geolocation must be
          'allowed' on your device.
        </p>
      </div>
    </template>

    <template v-else-if="defaultView === false && validSearch === true">
      <div class="slide-image">
        <img class="image" v-if="imageId === 1" src="../assets/1.png" alt="" />
        <img class="image" v-if="imageId === 2" src="../assets/2.png" alt="" />
        <img class="image" v-if="imageId === 3" src="../assets/3.png" alt="" />
        <img class="image" v-if="imageId === 4" src="../assets/4.png" alt="" />
        <img class="image" v-if="imageId === 5" src="../assets/5.png" alt="" />
        <div class="slide-content">
          <h2>Air Quality: {{ aqiLevelDisplay }}</h2>
          <div class="results">
            <ul class="results-grid">
              <li
                class="results-list-item"
                v-for="(level, pollutant) in pollutants"
                :key="level"
              >
                <span class="pollutant-name">{{
                  pollutant.toUpperCase()
                }}</span>
                : <span class="pollutant-level">{{ level }}</span>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </template>

    <template v-else-if="defaultView === false && validSearch === false">
      <div class="slide-image">
        <img class="image" src="../assets/error.png" alt="" />
      </div>
      <div class="slide-content">
        <h2>Whoops!</h2>
        <p class="results">
          Looks like there was an error getting that result. Very likely the
          search query you made does not match a city or location on the
          database. Give it another go!
        </p>
      </div>
    </template>
  </div>
</template>

<script>
export default {
  name: "CarouselSlide",
  props: ["aqi", "pollutants", "validSearch", "defaultView"],
  data() {
    return {
      imageId: null,
    };
  },

  computed: {
    aqiLevelDisplay() {
      if (this.aqi === 1) {
        this.imageId = 1;
        return "Good";
      }
      if (this.aqi === 2) {
        this.imageId = 2;
        return "Fair";
      }
      if (this.aqi === 3) {
        this.imageId = 3;
        return "Moderate";
      }
      if (this.aqi === 4) {
        this.imageId = 4;
        return "Poor";
      }
      if (this.aqi === 5) {
        this.imageId = 5;
        return "Very Poor";
      }
    },
  },
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
  padding: 0.5rem 0;
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
  color: rgb(4, 154, 255);
}
.pollutant-level {
  font-weight: bolder;
}
</style>
