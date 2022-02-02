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
          <a href="#" @click="getData"
            ><img class="icon" src="./assets/place.png" alt=""
          /></a>
          <form>
            <input placeholder="Search..." type="text" name="" id="" />
          </form>
          <a href="#"><img class="icon" src="./assets/search.png" alt="" /></a>
        </div>
        <div class="location-id">
          <p>Showing results for: Goole</p>
        </div>
      </div>
      <div class="carousel-container">
        <Slide />
      </div>
      <div class="cta">
        <button class="btn btn-cta">Refresh</button>
        <p class="cta-subdeck">Swipe to view more</p>
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
      lat: 0,
      lon: 0,
      co: 0,
      nh3: 0,
      no: 0,
      no2: 0,
      o3: 0,
      pm2_5: 0,
      pm10: 0,
      so2: 0,
    };
  },
  methods: {
    getData() {},
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
