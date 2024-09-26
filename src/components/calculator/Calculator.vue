<script setup lang="ts">
import { ref } from "vue";
import BMIResult from "./BMIResult.vue";
import ImperialPanel from "./ImperialPanel.vue";
import MetricPanel from "./MetricPanel.vue";
import UnitInput from "./UnitInput.vue";

const unit = ref<"metric" | "imperial">("metric");

// Metric units
const cm = ref(0);
const kg = ref(0);

// Imperial units
const ft = ref(0);
const inch = ref(0);
const st = ref(0);
const lbs = ref(0);
</script>

<template>
  <div
    class="shadowed absolute -bottom-8 left-1/2 flex w-full -translate-x-1/2 translate-y-full flex-col gap-6 rounded-2xl bg-white p-6 xl:gap-8 xl:p-8"
  >
    <h3 class="heading-m">Enter your details below</h3>
    <UnitInput v-model="unit" />

    <MetricPanel v-model:cm="cm" v-model:kg="kg" v-if="unit === 'metric'" />
    <ImperialPanel
      v-model:ft="ft"
      v-model:inch="inch"
      v-model:st="st"
      v-model:lbs="lbs"
      v-if="unit === 'imperial'"
    />

    <BMIResult
      v-model:cm="cm"
      v-model:kg="kg"
      v-model:ft="ft"
      v-model:inch="inch"
      v-model:st="st"
      v-model:lbs="lbs"
      v-model:unit="unit"
    />
  </div>
</template>

<style lang="sass" scoped>
.shadowed
  box-shadow: 16px 32px 56px 0px rgba(143, 174, 207, 0.25)
</style>
