<script setup lang="ts">
import { ERulesCalories } from '@/enums';
import { EDataCalories } from '@/enums';

defineProps({
  totalCalories: {
    type: Object,
    default: () => ({}),
  },
});
</script>

<template>
  <div
    class="flex mb-2"
    :class="{ 'text-red-600 !font-bold': totalCalories[key] > ERulesCalories[key as any] }"
    v-for="(val, key) in EDataCalories"
    :key="key"
  >
    <span v-if="val !== EDataCalories.weight" class="w-[10rem]">{{ val }} ({{ ERulesCalories[key as any] }}г.):</span>
    <span v-if="val !== EDataCalories.weight">{{ totalCalories[key] || 0 }}</span>
  </div>
</template>
<style scoped></style>
