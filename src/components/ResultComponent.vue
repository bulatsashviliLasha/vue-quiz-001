<template>
  <div class="results">
    <p>Your Results...</p>
    <h1>
      {{ props.questionStatus.numberOfCorrectAnswers }}/{{
        props.questionStatus.quantity
      }}
    </h1>
    <router-link to="/">Go Back</router-link>
  </div>
</template>

<script setup>
const props = defineProps(["questionStatus"]);
</script>

<style scoped>
.results {
  text-align: center;
  padding: 100px 0;
}
p {
  font-size: 25px;
}

h1 {
  font-size: 80px;
}
</style>
