<script setup>
import { defineProps } from 'vue';
import { RouterLink } from 'vue-router';

const { quizQuestionLength, numberOfCorrenctAnswers } = defineProps([
    'quizQuestionLength',
    'numberOfCorrenctAnswers',
]);
</script>

<template>
    <div class="results">
        <p>Your results...</p>
        <h1>{{ numberOfCorrenctAnswers }}/{{ quizQuestionLength }}</h1>
        <RouterLink to="/">Go Back</RouterLink>
    </div>
</template>

<style scoped>
.results {
    text-align: center;
    padding: 100px 0px;
}

p {
    font-size: 25px;
}

h1 {
    font-size: 80px;
}
</style>
