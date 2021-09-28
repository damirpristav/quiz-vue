<template>
  <div class="card">
    <div class="card-content">
      <div class="content">
        <h2 class="mb-5">{{ data.question }}</h2>
        <div class="control">
          <label class="radio has-background-light" v-for="choice in data.choices" :key="choice">
            <input type="radio" :value="choice" v-model="answer" />
            {{ choice }}
          </label>
        </div>
        <div class="has-text-danger" v-if="error">{{ error }}</div>
        <button class="button is-link is-medium is-fullwidth mt-4" @click="handleNext">Next</button>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  props: ['data'],
  setup(props, context) {
    const answer = ref('')
    const error = ref('')

    // On next button click
    const handleNext = () => {
      error.value = ''
      if(answer.value === '') {
        return error.value = 'Please select one option!'
      }
      context.emit('answerSubmit', answer.value)
      answer.value = ''
    }

    return { answer, handleNext, error }
  }
}
</script>

<style>

</style>