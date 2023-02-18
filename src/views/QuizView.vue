<script setup>
import Question from '../components/Question.vue';
import QuizHeader from '../components/QuizHeader.vue';
import Result from '../components/Result.vue';
import { useRoute } from 'vue-router';
import { ref, watch, computed } from 'vue';
import quizzes from '../data/quizzes.json';

const route = useRoute();
const quizId = parseInt(route.params.id);
const quiz = quizzes.find((q) => q.id === quizId);
const currentQuestionIndex = ref(0);
const numberOfCorrenctAnswers = ref(0);
const showResults = ref(false);

// Zmiana numerków pytań
const questionStatus = computed(
    () => `${currentQuestionIndex.value}/${quiz.questions.length}`
);

// Zmiana paska postępu
const barPercentage = computed(() => {
    return `${(currentQuestionIndex.value / quiz.questions.length) * 100}%`;
});

const onOptionSelected = (isCorrect) => {
    if (isCorrect) {
        numberOfCorrenctAnswers.value++;
    }

    if (quiz.questions.length - 1 === currentQuestionIndex.value) {
        showResults.value = true;
    }

    currentQuestionIndex.value++;
};
</script>

<template>
    <div>
        <QuizHeader
            :questionStatus="questionStatus"
            :barPercentage="barPercentage"
        />

        <div>
            <Question
                v-if="!showResults"
                :question="quiz.questions[currentQuestionIndex]"
                @selectOption="onOptionSelected"
            />

            <Result
                v-else
                :quizQuestionLength="quiz.questions.length"
                :numberOfCorrenctAnswers="numberOfCorrenctAnswers"
            />
        </div>
    </div>
</template>

<style scoped></style>
