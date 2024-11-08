<template>
  <v-container class="container">
    <v-btn
      value="rectangle"
      icon="mdi-rectangle-outline"
      size="large"
      @click="selectedShape = 'rectangle'"
      style="width: 50px; height: 50px; border-radius: 0"
    ></v-btn>
    <v-btn
    value="circle"
    icon="mdi-circle-outline"
    size="large"
    @click="selectedShape = 'circle'"
    style="width: 50px; height: 50px; border-radius: 0"
    ></v-btn>
    <CirclePan v-if="selectedShape === 'circle'" />
    <RectangulatPan v-if="selectedShape === 'rectangle'" />
  </v-container>
</template>

<script setup>
import { ref } from "vue";
import CirclePan from "./CirclePan.vue";
import RectangulatPan from "./RectangulatPan.vue";

const selectedShape = ref("circle");
</script>

<style lang="css" scoped>
.container {
  max-width: 300px;
}
</style>
