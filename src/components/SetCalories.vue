<script setup lang="ts">
import { EDataCalories } from '@/enums';
import { type ICalories } from '@/interfaces';

const setCalories: any = defineModel<Omit<ICalories, 'name'>>('setCalories');
</script>
<template>
  <div class="flex items-center mb-2" v-for="(val, key) in EDataCalories" :key="key">
    <span class="w-[11rem]">{{ val }}: </span>
    <input
      v-if="val === EDataCalories.name"
      v-model="setCalories[key]"
      type="text"
      placeholder="Название"
      class="input input-bordered input-sm input-info w-full max-w-xs rounded-[0.3rem] focus:outline-none"
    />
    <input
      v-if="val !== EDataCalories.name"
      v-model="setCalories[key]"
      type="number"
      min="0"
      placeholder="0"
      class="input input-bordered input-sm input-info w-full max-w-xs rounded-[0.3rem] focus:outline-none"
    />
  </div>
</template>
<style scoped>
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  /* display: none; <- Crashes Chrome on hover */
  -webkit-appearance: none;
  margin: 0; /* <-- Apparently some margin are still there even though it's hidden */
}
</style>
