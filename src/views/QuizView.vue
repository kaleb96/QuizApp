<script setup>
    import Question from '../components/Question.vue'
    import QuizHeader from '../components/QuizHeader.vue'
    import { useRoute } from 'vue-router';
    import { ref, watch, computed} from 'vue'
    import quizes from '../data/quizes.json'


    const route = useRoute()
    const quizId = parseInt(route.params.id);
    const currentQuestionIndex = ref(0);
    const quiz = quizes.find((q => q.id === quizId))



    /*Watch를 통해서 currentQuestionIndex를 감시하여 update하는 방법 
    const questionStatus = ref(`${currentQuestionIndex.value}/${quiz.questions.length}`)
    watch(() => currentQuestionIndex.value, () => {
        questionStatus.value = `${currentQuestionIndex.value}/${quiz.questions.length}`;
    })
    */
   
    /* computed를 통해서 currertQuestionIndex를 update하는 방법 
    const questionStatus =  computed(() => {   
        return `${currentQuestionIndex.value}/${quiz.questions.length}`
    })
    */
    const questionStatus =  computed(() => `${currentQuestionIndex.value}/${quiz.questions.length}`)

</script>

<template>
    <div>
        <quiz-header :questionStatus="questionStatus"/>
        <div>
            <question :question="quiz.questions[currentQuestionIndex]"/>
        </div>
        <button @click="currentQuestionIndex++">Next Question</button>
    </div> <!-- main div-->
</template>
  components: { QuizHeader },