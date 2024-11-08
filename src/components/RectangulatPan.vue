<template>
  <v-container class="container">
    <v-text-field
      clearable
      label="Height"
      v-model="heightValue"
      prepend-inner-icon="mdi-arrow-up"
      variant="outlined"
      :rules="[(value) => !!value || 'Required field']"
    ></v-text-field>
    <v-text-field
      clearable
      label="Length"
      v-model="lengthValue"
      prepend-inner-icon="mdi-arrow-right"
      variant="outlined"
      :rules="[(value) => !!value || 'Required field']"
    ></v-text-field>
    <v-text-field
      clearable
      v-model="widthValue"
      label="Width"
      prepend-inner-icon="mdi-arrow-left-right"
      variant="outlined"
      :rules="[(value) => !!value || 'Required field']"
    ></v-text-field>
  </v-container>
</template>

<script setup>
import { ref } from "vue";

const heightValue = ref("");
const widthValue = ref("");
const lengthValue = ref("");
</script>

<style lang="css" scoped>
.container {
  max-width: 300px;
}
</style>
