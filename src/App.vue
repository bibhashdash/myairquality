<template>
  <div class="app-container">
    <main>
      <div class="search">
        <div class="search-bar">
          <a href="#" @click="updateLocation"
            ><img class="icon" src="./assets/place.png" alt=""
          /></a>
          <form @submit.prevent="citySearch">
            <input
              placeholder="Search by city name..."
              type="text"
              name=""
              id=""
              v-model="citySearchString"
            />
          </form>
          <a href="#"
            ><img
              class="icon"
              src="./assets/search.png"
              alt=""
              @click.prevent="citySearch"
          /></a>
        </div>
      </div>

      <div class="carousel-container">
        <div class="location-id">
          <p v-if="validSearch === false">
            <span class="location-display">{{ currentLocationDisplay }}</span>
          </p>
          <p v-else-if="validSearch && currentLocationDisplay">
            <span class="location-display"
              >{{ currentLocationDisplay }}, {{ country }}</span
            >
          </p>
          <p v-else>
            <span class="location-display no-location">No location chosen</span>
          </p>
        </div>
        <Slide
          :aqi="aqi"
          :pollutants="pollutants"
          :validSearch="validSearch"
          :defaultView="defaultView"
        />
      </div>
      <div class="cta">
        <button class="btn btn-cta" @click.prevent="updateLocation">
          Device Location
        </button>
        <p class="footer-text">Copyright 2022 Bibhash Dash</p>
      </div>
    </main>
  </div>
</template>

<script>
import Slide from "./components/Slide.vue";
export default {
  name: "App",
  components: {
    Slide,
  },
  data() {
    return {
      citySearchString: "",
      lat: 0,
      lon: 0,
      pollutants: {},
      currentLocationDisplay: "",
      aqi: null,
      country: "",
      validSearch: true,
      defaultView: true,
    };
  },

  methods: {
    // fetch the air quality data
    maqData([x, y]) {
      (this.defaultView = false), (this.aqi = null);
      this.validSearch = true;

      fetch(
        `https://api.openweathermap.org/data/2.5/air_pollution?lat=${x}&lon=${y}&appid=d2a37cccedad8fffd47126ec42ab187f`
      )
        .then((response) => response.json())
        .then((data) => {
          console.log(data);
          this.aqi = data.list[0].main.aqi;
          // copy the pollutants data object from API to the pollutants object in data inside app component
          this.pollutants = JSON.parse(JSON.stringify(data.list[0].components));
        });
    },

    // getting coordinates from device location API
    // Using getCoords() to get latitude and longitude
    // then use await with updateLocation() to update data fields
    async getCoords() {
      return new Promise((resolve, reject) => {
        if (!navigator.geolocation) {
          reject("Geolocation unavailable on this device");
        }
        navigator.geolocation.getCurrentPosition(
          (position) => {
            // returning lat and lon as an array
            resolve([position.coords.latitude, position.coords.longitude]);
          },
          (error) => {
            reject(error);
          }
        );
      });
    },
    async updateLocation() {
      this.country = "";
      // destructuring array into lat and lon data fields
      [this.lat, this.lon] = await this.getCoords();
      this.maqData([this.lat, this.lon]);
      // reverse geocode to get the city name from the coordinates
      fetch(
        `https://api.openweathermap.org/geo/1.0/reverse?lat=${this.lat}&lon=${this.lon}&limit=1&appid=d2a37cccedad8fffd47126ec42ab187f`
      )
        .then((response) => response.json())
        .then((data) => {
          // console.log(data);
          this.currentLocationDisplay = data[0].name;

          this.country = data[0].country;
        });
    },

    // getting city coordinates from user string input
    citySearch() {
      this.validSearch = true;
      this.currentLocationDisplay = this.citySearchString;
      this.lat = 0;
      this.lon = 0;
      this.country = "";
      fetch(
        `https://api.openweathermap.org/geo/1.0/direct?q=${this.citySearchString}&limit=1&appid=d2a37cccedad8fffd47126ec42ab187f`
      )
        .then((response) => response.json())
        .then((data) => {
          // console.log(data);
          this.country = data[0].country;

          return [(this.lat = data[0].lat), (this.lon = data[0].lon)];
        })
        .then(([x, y]) => this.maqData([x, y]))
        .catch((error) => {
          this.currentLocationDisplay = "Invalid Search Query";
          this.validSearch = false;
          console.log(this.validSearch);
          return this.validSearch;
        });
      this.citySearchString = "";
    },
  },
};
</script>

<style>
#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  /* border: 1px solid red; */
  width: 100%;
}
.hidden {
  display: none;
}

h1,
h2,
h3,
h4,
h5,
h6,
a,
p {
  margin: 0;
  padding: 0;
}
p,
a {
  font-family: "Quicksand", sans-serif;
}

main {
  display: grid;
  grid-template-rows: auto auto 10%;
  gap: 1rem;
}

.search-bar {
  display: grid;
  grid-template-columns: 10% 80% 10%;

  border: 1px solid rgb(190, 190, 190);
  justify-items: center;
  align-items: center;
  padding: 20px;
  border-radius: 30px;
  margin: 15px 0;
}
form,
input {
  width: 100%;
}
input {
  border: none;
  margin: 0 5px;
  font-family: "Quicksand", sans-serif;
}
input:focus {
  outline: none;
}
.icon {
  width: 15px;
  opacity: 0.7;
}
.location-id {
  padding: 0 20px;
  text-align: center;
  margin-bottom: 10px;
}
.location-id p {
  font-weight: bolder;
}
.location-display {
  color: rgb(4, 154, 255);
  font-size: 1.5rem;
}
.no-location {
  font-weight: lighter;
  font-size: smaller;
  color: rgb(149, 149, 149);
}
.cta {
  display: flex;
  flex-direction: column;
  align-items: center;
  /* border: 1px solid red; */
  margin-top: 20px;
}
.btn {
  width: 70%;
  padding: 12px 15px;
  border-radius: 5px;
  margin-bottom: 1rem;
  border: none;
  font-family: "Quicksand", sans-serif;
  background: -webkit-linear-gradient(
    bottom,
    rgb(0, 215, 253),
    rgb(4, 163, 255)
  );
  font-weight: bolder;
}

.footer-text {
  font-size: 0.5rem;
  color: rgb(179, 179, 179);
}
</style>
