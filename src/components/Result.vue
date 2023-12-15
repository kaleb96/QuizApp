<script setup>

import {defineProps} from 'vue'
import {RouterLink} from 'vue-router'

const { numberOfCorrectAnswers, quizQuestionLength} = defineProps(['numberOfCorrectAnswers', 'quizQuestionLength'])
</script>

<template>
    <div class="results">
        <p>Your Results...</p>
        <h1>
            {{numberOfCorrectAnswers}}/{{quizQuestionLength}}
        </h1>
        <router-link to="/">Go Back</router-link>
    </div>
</template>

<style scopec>

.results {
    text-align: center;
    padding: 100px 0;
}

p {
    font-size: 25px;
}

h1{

    font-size:80px;
}
</style>