<script setup>
import { computed, reactive, ref } from "vue";
import { useRoute } from "vue-router";

import QuestionComponent from "@/components/QuestionComponent.vue";
import QuizHeader from "@/components/QuizHeader.vue";
import ResultComponent from "@/components/ResultComponent.vue";
import quizes from "@/data/data.json";

const route = useRoute();
const quizId = +route.params.id;
const quiz = quizes.find((q) => q.id === quizId);
const showResults = ref(false);

const questionStatus = reactive({
  currentQuestionIndex: 0,
  quantity: quiz.questions.length,
  numberOfCorrectAnswers: 0,
});

const barPercentage = computed(
  () =>
    (questionStatus.currentQuestionIndex / questionStatus.quantity) * 100 + "%"
);

const onOptionSelected = (isCorrect) => {
  if (isCorrect) {
    questionStatus.numberOfCorrectAnswers++;
  }

  if (questionStatus.quantity - 1 === questionStatus.currentQuestionIndex) {
    showResults.value = true;
  }

  questionStatus.currentQuestionIndex++;
};
</script>

<template>
  <div>
    <QuizHeader
      :questionStatus="questionStatus"
      :barPercentage="barPercentage"
    />
    <div>
      <QuestionComponent
        v-if="!showResults"
        @selectOption="onOptionSelected"
        :question="quiz.questions[questionStatus.currentQuestionIndex]"
      />
      <ResultComponent v-else :questionStatus="questionStatus" />
    </div>
  </div>
</template>
