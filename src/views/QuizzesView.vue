<script setup>
import CardComponent from "@/components/CardComponent.vue";
import q from "@/data/data.json";

import gsap from "gsap";

import { ref, watch } from "vue";
const search = ref("");
const quizes = ref(q);

watch(search, () => {
  quizes.value = q.filter((quiz) =>
    quiz.name.toLowerCase().includes(search.value.toLowerCase())
  );
});

const beforeEnter = (el) => {
  console.log("Before enter");
  el.style.opacity = 0;
  el.style.transform = "translateY(-100px)";
};
const afterEnter = (el) => {
  el.style.opacity = 1;
  el.style.transform = "translateY(0)";
};
const enter = (el) => {
  gsap.to(el, {
    y: 0,
    opacity: 1,
    duration: el.dataset.index,
  });
};
</script>

<template>
  <div>
    <header>
      <h1>Quizes</h1>
      <input v-model.trim="search" type="text" placeholder="Search..." />
    </header>
    <div class="options-container">
      <TransitionGroup
        appear
        @before-enter="beforeEnter"
        @after-enter="afterEnter"
        @enter="enter"
      >
        <CardComponent
          v-for="(quiz, index) in quizes"
          :key="quiz.id"
          :quiz="quiz"
          :data-index="(index + 1) / 1.9"
        />
      </TransitionGroup>
    </div>
  </div>
</template>

<style scoped>
.options-container {
  display: flex;
  flex-wrap: wrap;
  margin-top: 40px;
  justify-content: center;
}
</style>
