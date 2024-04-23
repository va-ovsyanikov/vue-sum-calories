<script setup lang="ts">
import { EDataCalories } from '@/enums';
const setCalories: any = defineModel('setCalories');
</script>
<template>
  <div class="mt-4 ml-2 p-2">
    <div class="flex mb-2" v-for="(val, key) in EDataCalories" :key="key">
      <span class="w-[7rem]">{{ val }}: </span>
      <input class="protein border-2 pl-0.5" v-model="setCalories[key]" type="number" min="0" placeholder="0" />
    </div>
  </div>
</template>
<style lang="scss" scoped></style>
