<script setup lang="ts">
import IconEating from "./icons/IconEating.vue";
import IconExercise from "./icons/IconExercise.vue";
import IconSleep from "./icons/IconSleep.vue";

defineProps<{
  title: string;
}>();
</script>

<template>
  <IconEating v-if="title === 'Healthy eating'" />
  <IconExercise v-else-if="title === 'Regular exercise'" />
  <IconSleep v-else />
</template>
