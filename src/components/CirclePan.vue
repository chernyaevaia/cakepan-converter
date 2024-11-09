<template>
  <v-container class="container">
    <v-text-field
      clearable
      label="Width"
      v-model="dimensions.diameter"
      @input="updateDimensions(dimensions)"
      prepend-inner-icon="mdi-arrow-left-right"
      variant="outlined"
      :rules="[(value) => !!value || 'Required field']"
    ></v-text-field>
    <v-text-field
      clearable
      v-model="dimensions.height"
      @input="updateDimensions(dimensions)"
      label="Diameter"
      prepend-inner-icon="mdi-diameter-outline"
      variant="outlined"
      :rules="[(value) => !!value || 'Required field']"
    ></v-text-field>
  </v-container>
</template>

<script setup>
import { defineProps, defineEmits } from "vue";
const { dimensions } = defineProps(["dimensions"]);
const emit = defineEmits();

function updateDimensions(dimensions) {
  emit("update-circle-dimensions", {
    diameter: dimensions.diameter,
    height: dimensions.height,
  });
}
</script>

<style lang="css" scoped>
.container {
  max-width: 300px;
}
</style>
