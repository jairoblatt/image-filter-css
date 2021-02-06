<template>
  <v-card class="d-flex justify-center py-2">
    <img class="preview-image" :style="imageFilterStyle" :src="imagePath" alt="Preview Image" />
  </v-card>
</template>
<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
  props: {
    imagePath: String,
    hueRotate: Number,
  },

  computed: {
    imageFilterStyle() {
      return {
        filter: `hue-rotate(${this.hueRotate}deg)`,
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
