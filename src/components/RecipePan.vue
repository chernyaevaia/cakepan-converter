<template>
  <v-container class="container">
    <div class="selection-row">
      <span class="selection-text">Choose recipe pan shape:</span>
      <div class="button-group">
        <v-btn
          value="rectangle"
          icon="mdi-rectangle-outline"
          size="large"
          @click="changeShape('rectangle')"
          :class="['shape-btn', getButtonClass('rectangle')]"
          class="shape-btn"
        ></v-btn>
        <v-btn
          value="circle"
          icon="mdi-circle-outline"
          size="large"
          @click="changeShape('circle')"
          :class="['shape-btn', getButtonClass('circle')]"
          class="shape-btn"
        ></v-btn>
      </div>
    </div>

    <CirclePan
      v-if="selectedRecipeShape === 'circle'"
      :dimensions="circleRecipePan"
      @update-circle-dimensions="updateCircleTarget"
    />
    <RectangularPan
      v-if="selectedRecipeShape === 'rectangle'"
      :dimensions="rectangleRecipePan"
      @update-rectangle-dimensions="updateRectangleTarget"
    />
  </v-container>
</template>

<script setup>
import { defineProps, defineEmits, computed } from "vue";
import CirclePan from "./CirclePan.vue";
import RectangularPan from "./RectangularPan.vue";

const props = defineProps({
  circleRecipePan: Object,
  rectangleRecipePan: Object,
  selectedRecipeShape: String,
});

const emit = defineEmits([
  "change-shape",
  "update-circle-dimensions",
  "update-rectangle-dimensions",
]);

const getButtonClass = computed(() => (shape) => {
  return props.selectedRecipeShape === shape ? "checked" : "";
});

function changeShape(newShape) {
  emit("change-shape", newShape);
}

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
  display: flex;
  flex-direction: column;
  margin: 0;
}

.selection-row {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 20px;
}

.selection-text {
  margin-right: 10px;
  white-space: nowrap;
}

.button-group {
  display: flex;
}

.shape-btn {
  max-width: 40px;
  max-height: 40px;
  border-radius: 0;
  margin: 0 5px;
}

.shape-btn.checked {
  background-color: #e0e0e0;
  box-shadow: inset 0 0 5px rgba(0, 0, 0, 0.2);
}
</style>
