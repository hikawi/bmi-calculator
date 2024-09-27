<script setup lang="ts">
import IconAge from "./icons/IconAge.vue";
import IconGender from "./icons/IconGender.vue";
import IconMuscle from "./icons/IconMuscle.vue";
import IconPregnancy from "./icons/IconPregnancy.vue";
import IconRace from "./icons/IconRace.vue";

defineProps<{
  title: string;
}>();
</script>

<template>
  <IconAge v-if="title === 'Age'" />
  <IconGender v-else-if="title === 'Gender'" />
  <IconMuscle v-else-if="title === 'Muscle'" />
  <IconPregnancy v-else-if="title === 'Pregnancy'" />
  <IconRace v-else />
</template>
