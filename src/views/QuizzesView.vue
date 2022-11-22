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
  el.style.opacity = 0;
  el.style.transform = "translateY(-70px)";
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
      <h1><img @click="$router.push('/')" src="../assets/Q.png" alt="Logo"></h1>
      <div>
        <input v-model.trim="search" type="text" placeholder="Search..." />
      </div>
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

      <section v-if="!quizes.length">
        <div>No Quiz found</div>
        <div @click="search = '' ">Back to Quizzes</div>
      </section>
    </div>
  </div>
</template>

<style scoped>
header h1 img{
  width: 75px;
  height: 75px;
  margin-left: 5px;
  cursor: pointer;
}
header div{
  display: flex;
  justify-content: center;
}
.options-container {
  display: flex;
  flex-wrap: wrap;
  margin-top: 40px;
  justify-content: center;
}
section{
  text-align: center;
  font-size: 30px;
  margin-top: 50px;
}
section div:last-child{
  cursor: pointer;
  font-weight: bold;
  font-size: 16px;
}
</style>
