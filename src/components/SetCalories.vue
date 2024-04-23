<script setup lang="ts">
import { EDataCalories } from '@/enums';
import { type ICalories } from '@/interfaces';

const setCalories: any = defineModel<ICalories>('setCalories');
</script>
<template>
  <div class="flex mb-2" v-for="(val, key) in EDataCalories" :key="key">
    <span class="w-[7rem]">{{ val }}: </span>
    <input class="protein border-2 pl-0.5" v-model="setCalories[key]" type="number" min="0" placeholder="0" />
  </div>
</template>
<style lang="scss" scoped></style>
