<script setup>
const props = defineProps(["question"]);
const emit = defineEmits(["selectOption"]);

const emitSelectedOption = (isCorrect) => {
  emit("selectOption", isCorrect)
}
</script>

<template>
  <section class="question-container">
    <h1 class="question">{{ props.question?.text }}</h1>
  </section>
  <section class="options-container">
    <div
        v-for="option in question?.options"
        :key="option.id"
        class="option"
        @click="emitSelectedOption(option.isCorrect)"
    >
      <div class="option-label">{{ option?.label }}</div>
      <div class="option-value">
        <div>{{ option?.text }}</div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.question-container {
  margin-top: 20px;
}

.question {
  font-size: 40px;
  margin-bottom: 20px;
}

.option {
  display: flex;
  margin-bottom: 20px;
  cursor: pointer;
}

.option-label {
  background-color: bisque;
  width: 50px;
  height: 50px;
  font-size: 30px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.option-value {
  background-color: rgb(244, 239, 239);
  width: 100%;
  font-size: 30px;
  padding: 0 20px;
}
</style>
