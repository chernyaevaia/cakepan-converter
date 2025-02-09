<template>
  <v-container class="container">
    <v-text-field
      clearable
      label="Height"
      v-model="dimensions.height"
      @input="updateDimensions(dimensions)"
      prepend-inner-icon="mdi-arrow-up"
      variant="outlined"
      :rules="[isValid]"
      type="number"
    ></v-text-field>
    <v-text-field
      clearable
      label="Length"
      v-model="dimensions.length"
      @input="updateDimensions(dimensions)"
      prepend-inner-icon="mdi-arrow-right"
      variant="outlined"
      :rules="[isValid]"
      type="number"
    ></v-text-field>
    <v-text-field
      clearable
      v-model="dimensions.width"
      @input="updateDimensions(dimensions)"
      label="Width"
      prepend-inner-icon="mdi-arrow-left-right"
      variant="outlined"
      :rules="[isValid]"
      type="number"
    ></v-text-field>
  </v-container>
</template>

<script setup>
import { defineProps, defineEmits, computed } from "vue";
const emit = defineEmits();
const { dimensions } = defineProps(["dimensions"]);

function updateDimensions(dimensions) {
  emit("update-rectangle-dimensions", {
    width: dimensions.width,
    height: dimensions.height,
    length: dimensions.length,
  });
}
const isValid = computed(() => (value) => !!value || "Required field");
</script>

<style lang="css" scoped>
.container {
  max-width: 300px;
  display: flex;
  flex-direction: column;
  row-gap: 16px;
}
</style>
