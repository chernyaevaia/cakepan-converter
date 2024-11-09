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
  <v-btn color="primary" variant="tonal">Convert</v-btn>
  <v-btn variant="tonal">Clear All</v-btn>
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
  circleRecipePan.diameter = newValues.diameter;
  circleRecipePan.height = newValues.height;
}
function updateCircleTarget(newValues) {
  circleTargetPan.diameter = newValues.diameter;
  circleTargetPan.height = newValues.height;
}

function updateRectangleRecipe(newValues) {
  rectangleRecipePan.width = newValues.width;
  rectangleRecipePan.height = newValues.height;
  rectangleRecipePan.length = newValues.length;
}

function updateRectangleTarget(newValues) {
  rectangleTargetPan.width = newValues.width;
  rectangleTargetPan.height = newValues.height;
  rectangleTargetPan.length = newValues.length;
}
</script>

<style lang="css" scoped>
.main-container {
  display: flex;
  padding: 50px 100px;
}
</style>
