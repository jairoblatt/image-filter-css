<template>
  <v-card outlined class="d-flex justify-center py-2">
    <img class="preview-image" :src="imagePath" :style="imageFilterStyle" alt="Preview Image" />
  </v-card>
</template>
<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
  props: {
    imagePath: String,
    hueRotate: Number,
    blur: Number,
    brightness: Number,
    contrast: Number,
    grayscale: Number,
    invert: Number,
    opacity: Number,
    saturate: Number,
    sepia: Number,
  },

  computed: {
    imageFilterStyle() {
      return {
        filter: `hue-rotate(${this.hueRotate}deg)
                 brightness(${this.brightness}%)
                 blur(${this.blur}px)
                 contrast(${this.contrast}%)
                 grayscale(${this.grayscale}%)
                 invert(${this.invert}%)
                 opacity(${this.opacity}%)
                 saturate(${this.saturate}%)
                 sepia(${this.sepia}%)`,
      };
    },
  },
});
</script>
<style scoped>
.preview-image {
  max-height: 500px;
}
</style>
