<template>
  <div class="location-id">
    <p v-if="currentLocationDisplay">
      <span class="location-display"
        >{{ currentLocationDisplay }}, {{ country }}</span
      >
    </p>
    <p v-else>
      <span class="location-display no-location">No location chosen</span>
    </p>
  </div>
</template>

<script>
export default {
  name: "LocationDisplay",
  props: ["currentLocationDisplay", "country", "validSearch"],
};
</script>

<style></style>
