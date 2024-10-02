<script setup lang="ts">
import { ref } from "vue";
import BMIResult from "./BMIResult.vue";
import ImperialPanel from "./ImperialPanel.vue";
import MetricPanel from "./MetricPanel.vue";
import UnitInput from "./UnitInput.vue";

const unit = ref<"metric" | "imperial">("metric");

// Metric units
const cm = ref<number | "">("");
const kg = ref<number | "">("");

// Imperial units
const ft = ref<number | "">("");
const inch = ref<number | "">("");
const st = ref<number | "">("");
const lbs = ref<number | "">("");
</script>

<template>
  <div
    class="shadowed flex h-full w-full flex-col gap-6 rounded-2xl bg-white p-6 xl:max-w-[35.25rem] xl:gap-8 xl:p-8"
  >
    <span class="heading-m">Enter your details below</span>
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
