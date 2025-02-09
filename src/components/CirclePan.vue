<template>
  <v-container class="container">
    <v-text-field
      clearable
      label="Diameter"
      v-model="dimensions.diameter"
      @input="updateDimensions(dimensions)"
      prepend-inner-icon="mdi-diameter-outline"
      variant="outlined"
      :rules="[isValid]"
      type="number"
    ></v-text-field>
    <v-text-field
      clearable
      label="Height"
      v-model="dimensions.height"
      @input="updateDimensions(dimensions)"
      prepend-inner-icon="mdi-arrow-up-down"
      variant="outlined"
      :rules="[isValid]"
      type="number"
    ></v-text-field>
  </v-container>
</template>

<script setup>
import { defineProps, defineEmits, computed } from "vue";

const { dimensions } = defineProps(["dimensions"]);
const emit = defineEmits();

function updateDimensions(dimensions) {
  emit("update-circle-dimensions", {
    diameter: dimensions.diameter,
    height: dimensions.height,
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

