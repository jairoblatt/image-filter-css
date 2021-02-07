<template>
  <v-col col="12">
    <v-card outlined class="d-flex justify-center align-center py-2 flex-column">
      <v-card-actions>
        <template v-if="loading">
          <v-progress-circular
            :size="50"
            color="deep-purple accent-4"
            indeterminate
          ></v-progress-circular>
        </template>
        <template v-else>
          <img
            class="preview-image"
            :src="imagePath"
            :style="{ filter: filterStyle }"
            alt="Preview Image"
          />
        </template>
      </v-card-actions>
      <v-card-actions>
        <v-btn @click="downloadImage" depressed color="deep-purple accent-4" class="white--text"
          >Download</v-btn
        >
      </v-card-actions>
      <v-card-text class="code-view">
        <span class="code-color-1"
          >filter: <span class="code-color-2">{{ filterStyle }};</span>
        </span>
      </v-card-text>
    </v-card>
  </v-col>
</template>
<script lang="ts">
import Vue from 'vue';

interface Data {
  loading: boolean;
}

interface Props {
  imagePath: string;
  hueRotate: number;
  blur: number;
  brightness: number;
  contrast: number;
  grayscale: number;
  invert: number;
  opacity: number;
  saturate: number;
  sepia: number;
}

interface Computed {
  filterStyle: string;
}

interface Methods {
  downloadImage: () => void;
  loadingToggle: () => void;
}

export default Vue.extend<Data, Methods, Computed, Props>({
  data: () => ({
    loading: false,
  }),

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
    filterStyle() {
      return `${this.blur ? `blur(${this.blur}px)` : ''}
              ${this.invert ? `invert(${this.invert}%)` : ''}
              ${this.sepia ? `sepia(${this.sepia}%)` : ''}
              ${this.hueRotate ? `hue-rotate(${this.hueRotate}deg)` : ''}
              ${this.grayscale ? `grayscale(${this.grayscale}%)` : ''}
              ${this.brightness !== 100 ? `brightness(${this.brightness}%)` : ''}
              ${this.contrast !== 100 ? `contrast(${this.contrast}%)` : ''}
              ${this.opacity !== 100 ? `opacity(${this.opacity}%)` : ''}
              ${this.saturate !== 100 ? `saturate(${this.saturate}%)` : ''}`;
    },
  },

  methods: {
    downloadImage() {
      const imageElement = document.createElement('a');
      imageElement.href = this.imagePath;
      imageElement.download = 'image.png';
      imageElement.click();
    },

    loadingToggle() {
      this.loading = !this.loading;
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
