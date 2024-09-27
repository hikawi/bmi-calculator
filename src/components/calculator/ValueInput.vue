<script setup lang="ts">
defineProps<{
  unit: string;
}>();

const value = defineModel<number | "">();
</script>

<template>
  <div
    class="group flex flex-1 flex-row items-center justify-between gap-2 rounded-xl border-[1px] border-dark-electric-blue bg-white px-6 py-5 focus-within:border-blue hover:border-blue xs:gap-6"
  >
    <input
      type="number"
      v-model="value"
      class="number-input heading-m w-full overflow-x-scroll outline-none"
    />
    <span class="heading-m shrink-0 text-blue">{{ unit }}</span>
  </div>
</template>

<style lang="sass" scoped>
.number-input
  -moz-appearance: textfield

  &::-webkit-inner-spin-button
    -webkit-appearance: none
    margin: 0

  &::-webkit-outer-spin-button
    -webkit-appearance: none
    margin: 0
</style>
