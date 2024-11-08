<template>
  <v-container class="main-container">
    <RecipePan />
    <TargetPan
  /></v-container>
  <v-btn color="primary" variant="tonal">Convert</v-btn>
  <v-btn variant="tonal">Clear All</v-btn>
</template>

<script setup>
import RecipePan from "./components/RecipePan.vue";
import TargetPan from "./components/TargetPan.vue";
</script>

<style lang="css" scoped>
.main-container {
  display: flex;
  padding: 50px 100px;
}
</style>
