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
</script>

<style lang="css" scoped>
.main-container {
  display: flex;
  padding: 50px 100px;
}
</style>
