<template>
  <v-container class="container">
    <div class="selection-row">
      <span class="selection-text">Choose your pan shape:</span>
      <div class="button-group">
        <v-btn
          icon="mdi-rectangle-outline"
          @click="changeShape('rectangle')"
          size="large"
          :class="['shape-btn', getButtonClass('rectangle')]"
          class="shape-btn"
        ></v-btn>
        <v-btn
          @click="changeShape('circle')"
          icon="mdi-circle-outline"
          size="large"
          :class="['shape-btn', getButtonClass('circle')]"
          class="shape-btn"
        ></v-btn>
      </div>
    </div>

    <CirclePan
      v-if="selectedTargetShape === 'circle'"
      :dimensions="circleTargetPan"
      @update-circle-dimensions="updateCircleTarget"
    />
    <RectangularPan
      v-if="selectedTargetShape === 'rectangle'"
      :dimensions="rectangleTargetPan"
      @update-rectangle-dimensions="updateRectangleTarget"
    />
  </v-container>
</template>

<script setup>
import { defineProps, defineEmits, computed } from "vue";
import CirclePan from "./CirclePan.vue";
import RectangularPan from "./RectangularPan.vue";

const props = defineProps({
  circleTargetPan: Object,
  rectangleTargetPan: Object,
  selectedTargetShape: String,
});

const emit = defineEmits([
  "update-circle-dimensions",
  "update-rectangle-dimensions",
  "change-shape",
]);

const getButtonClass = computed(() => (shape) => {
  return props.selectedTargetShape === shape ? "checked" : "";
});

function updateCircleTarget(dimensions) {
  emit("update-circle-dimensions", {
    diameter: dimensions.diameter,
    height: dimensions.height,
  });
}

function changeShape(newShape) {
  emit("change-shape", newShape);
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
