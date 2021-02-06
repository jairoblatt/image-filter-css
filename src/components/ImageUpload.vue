<template>
  <v-card outlined min-width="500px">
    <v-card-actions>
      <v-file-input
        v-model="imageFile"
        color="deep-purple accent-4"
        counter
        label="File input"
        multiple
        placeholder="Select your files"
        prepend-icon="mdi-paperclip"
        outlined
        :show-size="1000"
      >
        <template v-slot:selection="{ index, text }">
          <v-chip v-if="index < 2" color="deep-purple accent-4" dark label small>
            {{ text }}
          </v-chip>

          <span v-else-if="index === 2" class="overline grey--text text--darken-3 mx-2">
            +{{ files.length - 2 }} File(s)
          </span>
        </template>
      </v-file-input>
    </v-card-actions>
  </v-card>
</template>
<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
  data: () => ({
    imageFile: [],
  }),

  watch: {
    async imageFile(payload) {
      this.$emit('loading', true);
      try {
        const imageBase64 = await this.imageToBase64(payload[0]);
        this.$emit('imagePath', imageBase64);
      } catch (e) {
        console.error(e);
      } finally {
        setTimeout(() => {
          this.$emit('loading', false);
        }, 500);
      }
    },
  },

  methods: {
    imageToBase64(imageFile: File): Promise<string | void> {
      return new Promise((resolve, reject) => {
        const oFReader = new FileReader();
        oFReader.readAsDataURL(imageFile);
        oFReader.onload = (event) => resolve(event?.target?.result as string);
        oFReader.onerror = () => reject;
      });
    },

    // async createImageCanvas(imageBase64: string): Promise<HTMLCanvasElement> {
    //   const canvasElement = document.createElement('canvas');
    //   const imageElement = document.createElement('img');

    //   imageElement.src = imageBase64;
    //   canvasElement.width = imageElement.width;
    //   canvasElement.height = imageElement.height;

    //   canvasElement
    //     .getContext('2d')
    //     ?.drawImage(imageElement, 0, 0, canvasElement.width, canvasElement.height);
    //   console.log(canvasElement);
    //   return canvasElement;
    // },

    // scaleCanvasSize(canvas: HTMLCanvasElement, scale: number): HTMLCanvasElement {
    //   const scaledCanvas = document.createElement('canvas');
    //   scaledCanvas.height = canvas.height * scale;
    //   scaledCanvas.width = canvas.width * scale;
    //   scaledCanvas
    //     .getContext('2d')
    //     ?.drawImage(canvas, 0, 0, scaledCanvas.width, scaledCanvas.height);
    //   return scaledCanvas;
    // },
  },
});
</script>
