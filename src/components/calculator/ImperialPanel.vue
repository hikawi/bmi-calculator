<script setup lang="ts">
import ValueInput from "./ValueInput.vue";

const ft = defineModel<number | "">("ft");
const inch = defineModel<number | "">("inch");
const st = defineModel<number | "">("st");
const lbs = defineModel<number | "">("lbs");
</script>

<template>
  <div class="flex w-full flex-col gap-4 md:flex-row md:gap-6">
    <fieldset>
      <legend class="body-s mb-2 text-gunmetal">Height</legend>
      <div class="flex gap-4">
        <ValueInput v-model="ft" unit="ft" />
        <ValueInput v-model="inch" unit="in" />
      </div>
    </fieldset>

    <fieldset>
      <legend class="body-s mb-2 text-gunmetal">Weight</legend>
      <div class="flex gap-4">
        <ValueInput v-model="st" unit="st" />
        <ValueInput v-model="lbs" unit="lbs" />
      </div>
    </fieldset>
  </div>
</template>
