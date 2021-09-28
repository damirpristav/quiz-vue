<template>
  <div class="App">
    <Start v-if="step === 1" @startQuiz="handleStart" />
    <Question v-if="step === 2" :data="quizData.data[activeQuestion]" @answerSubmit="handleAnswer" />
    <End v-if="step === 3" :data="quizData.data" :results="answers" :time="time" @resetQuiz="handleReset" @showResults="showModal = true" />
    <Modal v-if="showModal" :results="answers" :data="quizData.data" @close="showModal = false" />
  </div>
</template>

<script>
import { ref } from 'vue'
import Start from './components/Start.vue'
import Question from './components/Question.vue'
import End from './components/End.vue'
import Modal from './components/Modal.vue'
import quizData from './data/quiz.json'

export default {
  name: 'App',
  components: { Start, Question, End, Modal },
  setup() {
    const step = ref(1)
    const time = ref(0)
    const activeQuestion = ref(0)
    const answers = ref([])
    const showModal = ref(false)
    let interval

    // On start
    const handleStart = () => {
      step.value = 2
      interval = setInterval(() => {
        time.value = time.value + 1
      }, 1000)
    }

    // On answer submit
    const handleAnswer = (answer) => {
      answers.value.push({ q: quizData.data[activeQuestion.value].question, a: answer })
      if(activeQuestion.value < quizData.data.length - 1) {
        activeQuestion.value = activeQuestion.value + 1
      }else {
        clearInterval(interval)
        step.value = 3
      }
    }

    // On reset
    const handleReset = () => {
      activeQuestion.value = 0
      time.value = 0
      answers.value = []
      step.value = 2
      interval = setInterval(() => {
        time.value = time.value + 1
      }, 1000)
    }

    return { step, handleStart, quizData, activeQuestion, handleAnswer, answers, time, handleReset, showModal }
  }
}
</script>

<style>
  html,
  body,
  #app {
    height: 100%;
  }

  .App {
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 100%;
  }

  .App .card {
    max-width: 400px;
    width: 100%;
    text-align: center;
  }

  label.radio {
    display: block;
    text-align: left;
    padding: 15px;
    margin-bottom: 5px;
    font-size: 20px;
  }

  label.radio+.radio {
    margin-left: 0;
  }

  label.radio input {
    margin-right: 10px;
  }
</style>
