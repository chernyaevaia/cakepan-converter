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
    <CirclePan
      v-if="selectedShape === 'circle'"
      :dimensions="circleRecipePan"
      @update-circle-dimensions="updateCircleTarget"
    />
    <RectangularPan
      v-if="selectedShape === 'rectangle'"
      :dimensions="rectangleRecipePan"
      @update-rectangle-dimensions="updateRectangleTarget"
    />
  </v-container>
</template>

<script setup>
import { ref, defineProps, defineEmits } from "vue";
import CirclePan from "./CirclePan.vue";
import RectangularPan from "./RectangularPan.vue";
const emit = defineEmits();

const { circleRecipePan, rectangleRecipePan } = defineProps([
  "circleRecipePan",
  "rectangleRecipePan",
]);

const selectedShape = ref("circle");
function updateCircleTarget(dimensions) {
  emit("update-circle-dimensions", {
    diameter: dimensions.diameter,
    height: dimensions.height,
  });
}

function updateRectangleTarget(dimensions) {
  emit("update-rectangle-dimensions", {
    width: dimensions.width,
    height: dimensions.height,
    length: dimensions.length,
  });
}
</script>

<style lang="css" scoped>
.container {
  max-width: 300px;
}
</style>
