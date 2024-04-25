<script setup lang="ts">
import { reactive, ref, watch, onMounted } from 'vue';
import { type ICalories } from '@/interfaces';
import SetCalories from '@/components/SetCalories.vue';
import ResultsCalories from '@/components/ResultsCalories.vue';

const key = ref(0);
const totalCalories = ref({} as ICalories);
const setCalories = reactive<Omit<ICalories, 'name'>>({
  protein: 0,
  fats: 0,
  carbohydrates: 0,
  kilocalories: 0,
  weight: 0,
});
const resultCalories = reactive({
  protein: 0,
  fats: 0,
  carbohydrates: 0,
  kilocalories: 0,
});
const onSetCalories = () => {
  if (confirm('Добавить данные?')) {
    resultCalories.protein =
      Math.round((setCalories.weight * setCalories.protein) / 100) + (totalCalories.value?.protein || 0);
    resultCalories.fats = Math.round((setCalories.weight * setCalories.fats) / 100) + (totalCalories.value?.fats || 0);
    resultCalories.carbohydrates =
      Math.round((setCalories.weight * setCalories.carbohydrates) / 100) + (totalCalories.value?.carbohydrates || 0);
    resultCalories.kilocalories =
      Math.round((setCalories.weight * setCalories.kilocalories) / 100) + (totalCalories.value?.kilocalories || 0);
    localStorage.setItem('calories', JSON.stringify(resultCalories));
    key.value++;
    setCalories.protein = 0;
    setCalories.fats = 0;
    setCalories.carbohydrates = 0;
    setCalories.kilocalories = 0;
    setCalories.weight = 0;
  }
};
const onResetCalories = () => {
  if (confirm('Вы действительно хотите сбросить данные?')) {
    localStorage.removeItem('calories');
    key.value++;
  }
};
watch(key, () => {
  totalCalories.value = JSON.parse(localStorage.getItem('calories') as string) || {};
});
onMounted(() => {
  totalCalories.value = JSON.parse(localStorage.getItem('calories') as string) || {};
});
</script>

<template>
  <main class="inline-block border-2">
    <div class="mt-4 ml-2 p-2">
      <a class="link link-secondary mb-4 block" href="https://calorizator.ru/" target="_blank"
        >Рецепты и калорийность продуктов</a
      >
      <SetCalories :setCalories="setCalories" />
      <button class="btn btn-success text-white h-[2rem] min-h-[2rem] rounded-[0.3rem]" @click="onSetCalories">
        Добавить
      </button>
    </div>
    <div class="mt-4 ml-2 p-2 mb-2">
      <ResultsCalories :totalCalories="totalCalories" />
      <button class="btn btn-error rounded-[0.3rem] text-white h-[2rem] min-h-[2rem]" @click="onResetCalories">
        Сбросить
      </button>
    </div>
  </main>
</template>

<style scoped></style>
