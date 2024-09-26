<script setup lang="ts">
import { computed } from "vue";

const props = defineProps<{
  ft: number | "";
  inch: number | "";
  st: number | "";
  lbs: number | "";
  kg: number | "";
  cm: number | "";
  unit: "imperial" | "metric";
}>();

function isInvalidNumber(value: number | "") {
  return (
    value === "" ||
    !Number.isSafeInteger(value) ||
    !Number.isFinite(value) ||
    value <= 0
  );
}

const error = computed(() => {
  if (props.unit === "imperial")
    return [props.ft, props.inch, props.st, props.lbs].some(isInvalidNumber);
  else return [props.cm, props.kg].some(isInvalidNumber);
});

function toFixed(num: number, precision: number): string {
  return (+(Math.round(+(num + "e" + precision)) + "e" + -precision)).toFixed(
    precision,
  );
}

// The formula for BMi is:
// kg/m^2 for metric
// lbs/in^2 * 703 for imperial
// But 1ft = 12in, 1st = 14lbs
const bmi = computed(() => {
  if (error.value) return 0;

  if (props.unit === "imperial") {
    const st = props.st as number;
    const lbs = props.lbs as number;
    const ft = props.ft as number;
    const inch = props.inch as number;
    return ((st * 14 + lbs) / (ft * 12 + inch) ** 2) * 703;
  }

  const kg = props.kg as number;
  const cm = props.cm as number;
  return kg / (cm / 100) ** 2;
});

/*
- Underweight: BMI less than 18.5
- Healthy weight: BMI 18.5 to 24.9
- Overweight: BMI 25 to 29.9
- Obese: BMI 30 or greater
*/
const status = computed(() => {
  if (bmi.value < 18.5) return "Underweight";
  if (bmi.value < 25) return "Healthy weight";
  if (bmi.value < 30) return "Overweight";
  return "Obese";
});

// To get the healthy range.
// For imperial: the formula is (lbs/inch^2) * 703 = bmi, therefore lbs = bmi * inch^2 / 703
// For metric: the formula is kg/m^2 = bmi, therefore kg = bmi * m^2
const healthyRange = computed(() => {
  if (props.unit === "imperial") {
    const inch = (props.ft as number) * 12 + (props.inch as number);
    const [min, max] = [(18.5 * inch ** 2) / 703, (24.9 * inch ** 2) / 703];

    const [minSt, minLbs] = [Math.floor(min / 14), Math.round(min % 14)];
    const [maxSt, maxLbs] = [Math.floor(max / 14), Math.round(max % 14)];
    return `${minSt}st ${minLbs}lbs - ${maxSt}st ${maxLbs}lbs`;
  }

  const cm = props.cm as number;
  const [min, max] = [18.5 * (cm / 100) ** 2, 24.9 * (cm / 100) ** 2];
  return `${toFixed(min, 1)}kgs - ${toFixed(max, 1)}kgs`;
});
</script>

<template>
  <div
    class="flex flex-col gap-6 rounded-2xl bg-blue p-8 text-white md:flex-row"
  >
    <div class="flex flex-col gap-2">
      <p class="body-m-bold">Your BMI is...</p>
      <span class="heading-l">{{ toFixed(bmi, 1) }}</span>
    </div>
  </div>
</template>
