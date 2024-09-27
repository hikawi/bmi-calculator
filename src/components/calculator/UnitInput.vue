<script setup lang="ts">
const unit = defineModel<"metric" | "imperial">();
</script>

<template>
  <div class="flex w-full flex-row gap-6">
    <label class="body-m-bold flex flex-1 flex-row items-center gap-4">
      <input
        type="radio"
        name="unit"
        value="metric"
        v-model="unit"
        class="radio"
      />
      Metric
    </label>
    <label class="body-m-bold flex flex-1 flex-row items-center gap-4">
      <input
        type="radio"
        name="unit"
        value="imperial"
        v-model="unit"
        class="radio"
      />
      Imperial
    </label>
  </div>
</template>

<style lang="sass" scoped>
.radio
  appearance: none
  -webkit-appearance: none
  @apply m-0 size-8 rounded-full border-[1px] border-[#6C9AA3]

  &:hover
    @apply border-blue

  &:checked
    @apply border-blue border-opacity-15 bg-blue bg-opacity-15 relative

    &:after
      content: ""
      @apply absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 size-4 rounded-full bg-blue
</style>
