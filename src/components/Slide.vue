<template>
  <div class="px-5">
    <v-subheader class="pl-0">{{ title }}</v-subheader>
    <v-slider dense v-bind="$attrs" @input="$emit('input', $event)" color="deep-purple accent-4">
      <template v-slot:append>
        <v-text-field
          v-model="$attrs.value"
          class="mt-0 pt-0"
          type="number"
          style="width: 60px"
        ></v-text-field>
      </template>
    </v-slider>
  </div>
</template>
<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
  props: {
    title: String,
  },
});
</script>
