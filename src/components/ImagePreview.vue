<template>
  <v-card outlined class="d-flex justify-center align-center py-2 flex-column">
    <v-card-actions>
      <img
        class="preview-image"
        :src="imagePath"
        :style="{ filter: imageFilterStyle }"
        alt="Preview Image"
      />
    </v-card-actions>
    <v-card-actions>
      <v-btn block depressed color="deep-purple accent-4" class="white--text">Download</v-btn>
    </v-card-actions>
    <v-card-text class="code-view">
      <span class="code-color-1">filter:</span>
      <span class="code-color-2">{{ imageFilterStyle }};</span>
    </v-card-text>
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
      return `${this.hueRotateFilter}
              ${this.blurFilter}
              ${this.brightnessFilter}
              ${this.contrastFilter}
              ${this.grayscaleFilter}
              ${this.invertFilter}
              ${this.opacityFilter}
              ${this.saturateFilter}
              ${this.sepiaFilter}`;
    },
    hueRotateFilter() {
      return this.hueRotate ? `hue-rotate(${this.hueRotate}deg)` : '';
    },

    blurFilter() {
      return this.blur ? `blur(${this.blur}px)` : '';
    },

    brightnessFilter() {
      return this.brightness !== 100 ? `brightness(${this.brightness}%)` : '';
    },

    contrastFilter() {
      return this.contrast !== 100 ? `contrast(${this.contrast}%)` : '';
    },

    grayscaleFilter() {
      return this.grayscale ? `grayscale(${this.grayscale}%)` : '';
    },

    invertFilter() {
      return this.invert ? `invert(${this.invert}%)` : '';
    },

    opacityFilter() {
      return this.opacity !== 100 ? `opacity(${this.opacity}%)` : '';
    },

    saturateFilter() {
      return this.saturate !== 100 ? `saturate(${this.saturate}%)` : '';
    },

    sepiaFilter() {
      return this.sepia ? `sepia(${this.sepia}%)` : '';
    },
  },
});
</script>
<style scoped>
.preview-image {
  max-height: 500px;
}

.code-view {
  background: #151718;
  border-radius: 7px;
  padding: 30px 20px;
  display: flex;
  width: 90%;
}
.code-color-1 {
  color: #38b0db;
  filter: blur(12);
}

.code-color-2 {
  color: #d9cd4f;
}
</style>
