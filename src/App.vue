<template>
  <v-container class="main-container">
    <RecipePan
      :circleRecipePan="circleRecipePan"
      :rectangleRecipePan="rectangleRecipePan"
      :selectedRecipeShape="selectedRecipeShape"
      @update-circle-dimensions="updateCircleRecipe"
      @update-rectangle-dimensions="updateRectangleRecipe"
      @change-shape="changeRecipeShape"
    />
    <TargetPan
      :circleTargetPan="circleTargetPan"
      :rectangleTargetPan="rectangleTargetPan"
      :selectedTargetShape="selectedTargetShape"
      @update-circle-dimensions="updateCircleTarget"
      @update-rectangle-dimensions="updateRectangleTarget"
      @change-shape="changeTargetShape"
    />
  </v-container>
  <div class="button-container">
    <v-btn variant="tonal" @click="clearAll">Clear All</v-btn>
    <v-btn
      color="primary"
      @click="calculateRatios"
      :disabled="!isAllFieldsFilled"
      >Convert</v-btn
    >
  </div>
  <div v-if="result !== null" class="result-container">
    <p>You need to multiply each ingredient by {{ result }}</p>
  </div>
</template>

<script setup>
import { reactive, ref, computed } from "vue";
import RecipePan from "./components/RecipePan.vue";
import TargetPan from "./components/TargetPan.vue";

const circleRecipePan = reactive({ diameter: "", height: "" });
const circleTargetPan = reactive({ diameter: "", height: "" });

const rectangleRecipePan = reactive({ width: "", length: "", height: "" });
const rectangleTargetPan = reactive({ width: "", length: "", height: "" });

const selectedTargetShape = ref("circle");
const selectedRecipeShape = ref("rectangle");
const result = ref(null);

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

function changeRecipeShape(newShape) {
  if (newShape === "circle") {
    Object.assign(rectangleRecipePan, { width: "", length: "", height: "" });
  } else {
    Object.assign(circleRecipePan, { diameter: "", height: "" });
  }
  selectedRecipeShape.value = newShape;
}

function changeTargetShape(newShape) {
  if (newShape === "circle") {
    Object.assign(rectangleTargetPan, { width: "", length: "", height: "" });
  } else {
    Object.assign(circleTargetPan, { diameter: "", height: "" });
  }
  selectedTargetShape.value = newShape;
}

function clearAll() {
  Object.assign(circleRecipePan, { diameter: "", height: "" });
  Object.assign(circleTargetPan, { diameter: "", height: "" });
  Object.assign(rectangleRecipePan, { width: "", length: "", height: "" });
  Object.assign(rectangleTargetPan, { width: "", length: "", height: "" });
  result.value = null;
}

const isAllFieldsFilled = computed(() => {
  const requiredFields = {
    circle: ["diameter", "height"],
    rectangle: ["width", "length", "height"],
  };

  const isFilled = (shape, pan) => {
    return requiredFields[shape].every((field) => {
      const value = pan[field];
      return value !== 0 && !isNaN(value);
    });
  };

  const recipeFilled = isFilled(
    selectedRecipeShape.value,
    selectedRecipeShape.value === "circle"
      ? circleRecipePan
      : rectangleRecipePan
  );

  const targetFilled = isFilled(
    selectedTargetShape.value,
    selectedTargetShape.value === "circle"
      ? circleTargetPan
      : rectangleTargetPan
  );

  return recipeFilled && targetFilled;
});

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

  const roundedRatio = Math.round(ratio * 100) / 100;

  result.value = roundedRatio;
}
</script>

<style lang="css" scoped>
.main-container {
  display: flex;
  min-height: 430px;
  box-sizing: border-box;
  justify-content: center;
  column-gap: 90px;
}

.button-container {
  display: flex;
  justify-content: center;
  padding: 20px;
  width: 100%;
}

.button-container .v-btn {
  margin: 0 10px;
}

.result-container {
  display: flex;
  justify-content: center;
  margin-top: 20px;
  font-size: 18px;
  font-weight: bold;
}
</style>
