<template>
  <div class="card">
    <div class="card-content">
      <div class="content">
        <h3>Your results</h3>
        <p>{{ correctAnswers }} of {{ data.length }}</p>
        <p><strong>{{Math.floor((correctAnswers / data.length) * 100)}}%</strong></p>
        <p><strong>Your time:</strong> {{ formatTime(time) }}</p>
        <button class="button is-info mr-2" @click="handleCheckAnswers">Check your answers</button>
        <button class="button is-success" @click="handleReset">Try again</button>
      </div>
    </div>
  </div>
</template>

<script>
import { computed } from 'vue'
import { formatTime } from '../utils'

export default {
  props: ['data', 'results', 'time'],
  setup({ data, results }, context) {
    // Get correct answers
    const correctAnswers = computed(() => {
      let correct = 0
      results.forEach((result, idx) => {
        if(result.a === data[idx].answer) {
          correct++
        }
      })
      return correct
    })

    // On check answer button click
    const handleCheckAnswers = () => {
      context.emit('showResults')
    }

    // On try again button click
    const handleReset = () => {
      context.emit('resetQuiz')
    }

    return { correctAnswers, handleCheckAnswers, handleReset, formatTime }
  }
}
</script>

<style>

</style>