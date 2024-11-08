<template>
  <v-container class="container">
    <v-text-field
      clearable
      label="Width"
      v-model="widthValue"
      prepend-inner-icon="mdi-arrow-left-right"
      variant="outlined"
       :rules="[(value) => !!value || 'Required field']"
    ></v-text-field>
    <v-text-field
      clearable
      label="Diameter"
      v-model="diameterValue"
      prepend-inner-icon="mdi-diameter-outline"
      variant="outlined"
      :rules="[(value) => !!value || 'Required field']"
    ></v-text-field>
  </v-container>
</template>

<script setup>
import { ref } from "vue";

const diameterValue = ref("");
const widthValue = ref("");
</script>

<style lang="css" scoped>
.container {
  max-width: 300px;
}
</style>
