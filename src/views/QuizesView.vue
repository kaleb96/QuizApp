<script setup>
  import q from '../data/quizes.json'
  import { ref, watch } from 'vue'
  import Card from '../components/Card.vue'
  import gsap from 'gsap';

  // state
  const quizes = ref(q);
  const search = ref('');
  // const showCards = ref(false);
  watch(search, () => {
    quizes.value = q.filter(quiz => quiz.name.toLowerCase().includes(search.value.toLowerCase()))
  })

  const beforeEnter = (el) => {
    // card-enter-from
    // el.style.opacity = 0;
    // el.style.transform = "translateY(-60px)"
    gsap.to(el, {
      y: -60,
      opacity: 0,
    })
  }
  
  const enter = (el) => {
    // card-enter-to
    // el.style.opacity = 1;
    // el.style.transform = "translateY(0)"
    gsap.to(el, {
      y: 0,
      opacity: 1,
      duration: 0.6,
      delay: el.dataset.index * 0.3
    })
  }

  const afterEnter = () => {

  }
</script>

<template>
    <div>
      <header>
        <h1>Quizes</h1>
        <input v-model.trim="search" type="text" placeholder="Search...">
      </header>

      <div class="options-container">
        <TransitionGroup 
          appear
          @before-enter="beforeEnter"
          @enter="enter"
        >
          <Card 
            v-for="(quiz, index) in quizes" 
            :key="quiz.id" 
            :quiz="quiz"
            :data-index="index"
            />
            <!-- v-if="showCards" -->
        </TransitionGroup>
        <!-- <button @click="showCards = !showCards">Show</button> -->
      </div>
    </div>
</template>

<style scoped>
  header {
    margin-bottom: 10px;
    margin-top: 30px;
    display: flex;
    align-items: center;
  }

  header h1 {
    font-weight: bold;
    margin-right: 30px;
  }

  header input {
    border: none;
    background-color: rgba(128,128,128,0.1);
    padding: 10px;
    border-radius: 5px;
  }

  .options-container {
    display: flex;
    flex-wrap: wrap;
    margin-top: 40px;
  }
/*
  .card-enter-from {
    transform: translateY(-50px);
    opacity: 0;
  }
  .card-enter-to {
    transform: translateY(0);
    opacity: 1;
  }
  .card-enter-active {
    transition: all 0.6s ease;
  } */
</style>