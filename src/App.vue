<template>
  <v-app>
    <v-container>
      <v-row>
        <v-col col="12" class="justify-center d-flex">
          <ImageUpload @imagePath="setImagePath" />
        </v-col>
      </v-row>
      <v-row>
        <v-col col="4">
          <ImagePreview :image-path="imagePath" :hue-rotate="testando" />
        </v-col>
        <v-col col="8" class="justify-center d-flex">
          <v-slider v-model="testando" min="0" max="360">
            <template v-slot:append>
              <v-text-field
                v-model="testando"
                class="mt-0 pt-0"
                type="number"
                style="width: 60px"
              ></v-text-field>
            </template>
          </v-slider>
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
  },

  data: () => ({
    testando: 0,
    imagePath: '',
  }),

  methods: {
    setImagePath(image64: string) {
      console.log(image64);
      this.imagePath = image64;
    },
  },
});
</script>
