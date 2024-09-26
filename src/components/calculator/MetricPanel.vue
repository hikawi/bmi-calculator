<script setup lang="ts">
import ValueInput from "./ValueInput.vue";

const cm = defineModel<number | "">("cm");
const kg = defineModel<number | "">("kg");
</script>

<template>
  <div class="flex w-full flex-col gap-4 md:flex-row md:gap-6">
    <label class="body-s flex w-full flex-col gap-2 text-gunmetal">
      Height
      <ValueInput v-model="cm" unit="cm" />
    </label>
    <label class="body-s flex w-full flex-col gap-2 text-gunmetal">
      Weight
      <ValueInput v-model="kg" unit="kg" />
    </label>
  </div>
</template>
