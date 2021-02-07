<template>
  <v-app>
    <v-container>
      <v-row>
        <v-col col="12" class="justify-center d-flex">
          <ImageUpload @imagePath="setImagePath" @loading="loadingImagePreview" />
        </v-col>
      </v-row>
      <v-row>
        <v-col col="12">
          <ImagePreview
            ref="imagePreview"
            :image-path="imagePath"
            :hue-rotate="hueRotate"
            :brightness="brightness"
            :contrast="contrast"
            :grayscale="grayscale"
            :invert="invert"
            :opacity="opacity"
            :saturate="saturate"
            :sepia="sepia"
            :blur="blur"
          />
        </v-col>
        <v-col col="8" class="justify-center d-flex">
          <v-col col="12">
            <v-card outlined>
              <Slide title="Hue-rotate" min="0" max="360" v-model="hueRotate" />
              <Slide title="Blur" min="0" max="100" v-model="blur" />
              <Slide title="Brightness" min="0" max="300" v-model="brightness" />
              <Slide title="Contrast" min="0" max="100" v-model="contrast" />
              <Slide title="Grayscale" min="0" max="100" v-model="grayscale" />
              <Slide title="Invert" min="0" max="100" v-model="invert" />
              <Slide title="Opacity" min="0" max="100" v-model="opacity" />
              <Slide title="Saturate" min="0" max="100" v-model="saturate" />
              <Slide title="Sepia" min="0" max="100" v-model="sepia" />
              <v-card-text>
                <v-btn
                  depressed
                  block
                  color="deep-purple accent-4"
                  class="white--text"
                  @click="resetAll"
                  >Reset all</v-btn
                >
              </v-card-text>
            </v-card>
          </v-col>
        </v-col>
      </v-row>
    </v-container>
  </v-app>
</template>

<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
  components: {
    ImageUpload: () => import('@/components/ImageUpload.vue'),
    ImagePreview: () => import('@/components/ImagePreview.vue'),
    Slide: () => import('@/components/Slide.vue'),
  },

  data: () => ({
    hueRotate: 0,
    blur: 0,
    brightness: 100,
    contrast: 100,
    grayscale: 0,
    invert: 0,
    opacity: 100,
    saturate: 100,
    sepia: 0,
    imagePath:
      'https://i.picsum.photos/id/894/536/354.jpg?hmac=nPb0JmJGnGKCyKy2womYYaVlNlraeMW2gbX8vdO-Lr4',
  }),

  methods: {
    setImagePath(image64: string) {
      this.imagePath = image64;
    },

    resetAll() {
      Object.assign(this.$data, (this.$options as any).data());
    },

    loadingImagePreview() {
      (this.$refs.imagePreview as Vue & { loadingToggle: () => void }).loadingToggle();
    },
  },
});
</script>
