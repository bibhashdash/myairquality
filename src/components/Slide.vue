<template>
  <div class="slide-wrapper">
    <div class="slide-image">
      <img class="image" src="../assets/monk.png" />
    </div>
    <div class="slide-content">
      <h2 class="slide-title">Ahhhh!</h2>
      <p class="slide-subdeck">
        Lorem ipsum dolor sit, amet consectetur adipisicing elit. Autem,
        corrupti omnis eligendi voluptates explicabo molestiae quae culpa
        ratione.
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "CarouselSlide",
  data() {
    return {};
  },
  methods: {},
};
</script>

<style>
.slide-wrapper {
  width: 100%;
  display: flex;
  flex-direction: column;
}
.slide-image {
  align-self: center;
  width: 70%;
  text-align: center;
}
.image {
  width: 100%;
}
.slide-content {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.slide-subdeck {
  text-align: center;
  padding: 10px 10%;
  font-size: 0.8rem;
}
</style>
