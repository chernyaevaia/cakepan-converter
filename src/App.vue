<template>
  <v-container class="main-container">
    <RecipePan
      :circleRecipePan="circleRecipePan"
      :rectangleRecipePan="rectangleRecipePan"
      @update-circle-dimensions="updateCircleRecipe"
      @update-rectangle-dimensions="updateRectangleRecipe" />
    <TargetPan
      :circleTargetPan="circleTargetPan"
      :rectangleTargetPan="rectangleTargetPan"
      @update-circle-dimensions="updateCircleTarget"
      @update-rectangle-dimensions="updateRectangleTarget"
  /></v-container>
  <v-btn color="primary" @click="calculateRatios" variant="tonal"
    >Convert</v-btn
  >
  <v-btn variant="tonal" @click="clearAll">Clear All</v-btn>
</template>

<script setup>
import RecipePan from "./components/RecipePan.vue";
import TargetPan from "./components/TargetPan.vue";
import { reactive } from "vue";

const circleRecipePan = reactive({ diameter: "", height: "" });
const circleTargetPan = reactive({ diameter: "", height: "" });

const rectangleRecipePan = reactive({ width: "", length: "", height: "" });
const rectangleTargetPan = reactive({ width: "", length: "", height: "" });

function updateCircleRecipe(newValues) {
  Object.assign(circleRecipePan, newValues);
}

function updateCircleTarget(newValues) {
  Object.assign(circleTargetPan, newValues);
}

function updateRectangleRecipe(newValues) {
  Object.assign(rectangleRecipePan, newValues);
}

function updateRectangleTarget(newValues) {
  Object.assign(rectangleTargetPan, newValues);
}

function clearAll() {
  Object.assign(circleRecipePan, { diameter: "", height: "" });
  Object.assign(circleTargetPan, { diameter: "", height: "" });
  Object.assign(rectangleRecipePan, { width: "", length: "", height: "" });
  Object.assign(rectangleTargetPan, { width: "", length: "", height: "" });
}

function calculateCircleVolume(circlePan) {
  const radius = circlePan.diameter / 2;
  const volume = Math.PI * Math.pow(radius, 2) * circlePan.height;
  const roundedVolume = Math.round(volume * 10) / 10;
  return roundedVolume;
}

function calculateRectangleVolume(rectanglePan) {
  const volume = rectanglePan.width * rectanglePan.height * rectanglePan.length;
  const roundedVolume = Math.round(volume * 10) / 10;
  return roundedVolume;
}

function calculateRatios() {
  const isfilledCircleRecipe =
    circleRecipePan.diameter && circleRecipePan.height;
  const isfilledCircleTarget =
    circleTargetPan.diameter && circleTargetPan.height;
  const isfilledRectangleRecipe =
    rectangleRecipePan.width &&
    rectangleRecipePan.length &&
    rectangleRecipePan.height;
  const isfilledRectangleTarget =
    rectangleTargetPan.width &&
    rectangleTargetPan.length &&
    rectangleTargetPan.height;

  const circleRecipeVolume = isfilledCircleRecipe
    ? calculateCircleVolume(circleRecipePan)
    : 0;
  const circleTargetVolume = isfilledCircleTarget
    ? calculateCircleVolume(circleTargetPan)
    : 0;
  const rectangleRecipeVolume = isfilledRectangleRecipe
    ? calculateRectangleVolume(rectangleRecipePan)
    : 0;
  const rectangleTargetVolume = isfilledRectangleTarget
    ? calculateRectangleVolume(rectangleTargetPan)
    : 0;

  const recipeVolume = circleRecipeVolume || rectangleRecipeVolume;
  const targetVolume = circleTargetVolume || rectangleTargetVolume;

  const ratio = targetVolume / recipeVolume;

  console.log(ratio);
}
</script>

<style lang="css" scoped>
.main-container {
  display: flex;
  padding: 50px 100px;
}
</style>
