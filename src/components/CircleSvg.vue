<template>
  <div class="svg-container">
    <!-- Dynamically load external SVG file -->
    <img :src="icon" alt="Circle icon" />
  </div>
</template>

<script>
// Import the SVG file from the assets folder
import CheckIcon from '@/assets/circle.svg';

export default {
  name: "CircleSvg",
  data() {
    return {
      icon: CheckIcon // The imported SVG file as the source
    };
  }
};
</script>

<style scoped>
.svg-container {
  width: 18px;
  height: 18px;
}

img {
  width: 100%; /* Ensures the image scales according to the container size */
  height: auto;
  display: block;
}
</style>
