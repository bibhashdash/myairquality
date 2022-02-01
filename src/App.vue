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
          <a href="#"><img class="icon" src="./assets/search.png" alt="" /></a>

          <form>
            <input placeholder="Search..." type="text" name="" id="" />
          </form>
          <a href="#"><img class="icon" src="./assets/place.png" alt="" /></a>
        </div>
        <div class="location-id">
          <p>Current Location: Goole</p>
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
};
</script>

<style>
#app {
  font-family: "Montserrat", sans-serif;
  display: flex;
  flex-direction: column;
  align-items: center;

  /* width: 90vw; */
  height: calc(100vh - 50px);
  /* border: 2px solid rgb(211, 72, 30); */
  /* overflow-y: scroll; */
}

.app-container {
  display: grid;
  height: 100%;
  grid-template-rows: 10% 90%;
  /* border: 2px solid rgb(13, 14, 20); */
}
h1,
h2,
h3,
h4,
h5,
h6 {
  padding: 0;
  margin: 0;
}
p,
a {
  margin: 0;
  padding: 0;
  font-family: "Quicksand", sans-serif;
}
header {
  width: 90%;
  padding: 0;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  align-self: center;
  /* margin-bottom: 3rem; */
}
.brand {
  width: auto;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.apptitle {
  margin: 0;
  font-size: 1rem;
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
  width: 60px;
  margin-right: 5px;
}
.modal {
  align-self: flex-end;
}

main {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-evenly;
}
.search {
  width: 90%;
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
.carousel-container {
  width: 90%;
  /* border: 1px solid rgba(0, 0, 0, 0.226); */

  /* margin-bottom: 2rem; */
}

.cta {
  width: 80%;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.btn {
  width: 70%;
  padding: 12px 15px;
  border-radius: 5px;
  /* margin-bottom: 1rem; */
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
