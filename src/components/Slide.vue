<template>
  <div class="carousel-wrapper">
    <div class="slide-image">
      <img class="image" src="../assets/monk.png" />
    </div>
    <div class="slide-content">
      <h2 class="slide-title">Current Level: Low</h2>
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
