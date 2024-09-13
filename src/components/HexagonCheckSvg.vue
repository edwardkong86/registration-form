<template>
  <div class="svg-container">
    <!-- Dynamically load external SVG file -->
    <img :src="icon" alt="Hexagon Check icon" />
  </div>
</template>

<script>
// Import the SVG file from the assets folder
import CheckIcon from '@/assets/hexagon-check.svg';

export default {
  name: "HexagonCheckSvg",
  data() {
    return {
      icon: CheckIcon // The imported SVG file as the source
    };
  }
};
</script>

<style scoped>
.svg-container {
  width: 24px;
  height: 24px;
}

img {
  width: 100%; /* Ensures the image scales according to the container size */
  height: auto;
  display: block;
}
</style>
