<script setup>
import CardComponent from "@/components/CardComponent.vue";
import q from "@/data/data.json";

import { ref, watch } from "vue";
const search = ref("");
const quizes = ref(q);

watch(search, () => {
  quizes.value = q.filter((quiz) =>
    quiz.name.toLowerCase().includes(search.value.toLowerCase())
  );
});
</script>

<template>
  <div>
    <header>
      <h1>Quizes</h1>
      <input v-model.trim="search" type="text" placeholder="Search..." />
    </header>
    <div class="options-container">
      <CardComponent v-for="quiz in quizes" :key="quiz.id" :quiz="quiz" />
    </div>
  </div>
</template>

<style scoped>
.options-container {
  display: flex;
  flex-wrap: wrap;
  margin-top: 40px;
}
</style>
