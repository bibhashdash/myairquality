<template>
  <div class="app-container">
    <header>
      <div class="brand">
        <img
          class="logo"
          src="../src/assets/maqlogo.png"
          alt="my air quality logo"
        />
        <h1 class="apptitle">My Air Quality</h1>
      </div>
      <div class="modal">
        <p>Readme</p>
      </div>
    </header>
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
              @click="citySearch"
          /></a>
        </div>
        <div class="location-id">
          <p v-if="currentLocationDisplay">
            Showing results for: {{ currentLocationDisplay }}
          </p>
          <p v-else>No location chosen</p>
        </div>
      </div>
      <div class="carousel-container">
        <Slide :aqi="aqi" />
      </div>
      <div class="cta">
        <button class="btn btn-cta" @click="updateLocation">
          Refresh current
        </button>
        <!-- <p class="cta-subdeck">Swipe to view more</p> -->
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
      no2: 0,
      o3: 0,
      pm2_5: 0,
      pm10: 0,
      so2: 0,
      currentLocationDisplay: "",
      aqi: null,
    };
  },

  methods: {
    // fetch the air quality data
    maqData([x, y]) {
      this.aqi = null;
      console.log(x, y);
      fetch(
        `http://api.openweathermap.org/data/2.5/air_pollution?lat=${x}&lon=${y}&appid=d2a37cccedad8fffd47126ec42ab187f`
      )
        .then((response) => response.json())
        .then((data) => {
          // console.log(data);
          this.aqi = data.list[0].main.aqi;
          console.log(this.aqi);
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
      // destructuring array into lat and lon data fields
      [this.lat, this.lon] = await this.getCoords();
      this.maqData([this.lat, this.lon]);
      // reverse geocode to get the city name from the coordinates
      fetch(
        `http://api.openweathermap.org/geo/1.0/reverse?lat=${this.lat}&lon=${this.lon}&limit=1&appid=d2a37cccedad8fffd47126ec42ab187f`
      )
        .then((response) => response.json())
        .then((data) => {
          this.currentLocationDisplay = data[0].name;
        });
    },

    // getting city coordinates from user string input
    citySearch() {
      this.currentLocationDisplay = this.citySearchString;
      this.lat = 0;
      this.lon = 0;
      fetch(
        `http://api.openweathermap.org/geo/1.0/direct?q=${this.citySearchString}&limit=1&appid=d2a37cccedad8fffd47126ec42ab187f`
      )
        .then((response) => response.json())
        .then((data) => {
          return [(this.lat = data[0].lat), (this.lon = data[0].lon)];
        })
        .then(([x, y]) => this.maqData([x, y]));
      this.citySearchString = "";
    },
  },
};
</script>

<style>
#app {
  padding: 0 1rem;
  font-family: "Montserrat", sans-serif;
  display: flex;
  flex-direction: column;
  align-items: center;

  height: 550px;
}
.hidden {
  display: none;
}
@media all and (min-height: 600px) and (max-height: 699px) {
  #app {
    height: 600px;
  }
}
@media all and (min-height: 700px) and (max-height: 799px) {
  #app {
    height: 700px;
  }
}
@media all and (min-height: 800px) and (max-height: 899px) {
  #app {
    height: 800px;
  }
}
@media all and (min-height: 900px) and (max-height: 999px) {
  #app {
    height: 900px;
  }
}
@media all and (min-height: 1000px) and (max-height: 1099px) {
  #app {
    height: 1000px;
  }
}

@media all and (min-height: 1100px) and (max-height: 1199px) {
  #app {
    height: 1100px;
  }
}
@media all and (min-height: 1200px) and (max-height: 1299px) {
  #app {
    height: 1200px;
  }
}
@media all and (min-height: 1300px) and (max-height: 1399px) {
  #app {
    height: 1300px;
  }
}
@media all and (min-height: 1400px) and (max-height: 1499px) {
  #app {
    height: 1400px;
  }
}
.app-container {
  display: grid;
  height: 100%;
  grid-template-rows: 10% 90%;
  gap: 2rem;
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
header {
  padding: 0;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  align-self: center;
}
.brand {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.apptitle {
  margin: 0;
  font-size: 0.5rem;
  font-weight: bolder;
  background: -webkit-linear-gradient(
    bottom,
    rgb(0, 253, 148),
    rgb(4, 154, 255)
  );
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.logo {
  width: 50px;
  margin-right: 5px;
}
.modal {
  align-self: flex-end;
  font-size: 0.8rem;
}

main {
  display: grid;
  gap: 1rem;
}

.search-bar {
  display: grid;
  grid-template-columns: 10% 80% 10%;

  border: 1px solid rgb(190, 190, 190);
  justify-items: center;
  align-items: center;
  padding: 10px;
  border-radius: 30px;
  margin: 0 0 5px;
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
}
.location-id p {
  font-weight: bolder;
}

.cta {
  display: flex;
  flex-direction: column;
  align-items: center;
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

.cta-subdeck {
  color: rgb(179, 179, 179);
}
</style>
