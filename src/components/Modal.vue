<template>
  <div class="modal is-active">
    <div class="modal-background" @click="handleClose"></div>
    <div class="modal-card">
      <header class="modal-card-head">
        <p class="modal-card-title">Your answers</p>
        <button class="delete" @click="handleClose"></button>
      </header>
      <section class="modal-card-body content">
        <ul>
          <li v-for="(result, i) in results" :key="result.a" class="mb-6">
            <p><strong>{{ result.q }}</strong></p>
            <p 
              class="has-text-white p-2" 
              :class="{ 'has-background-success': result.a === data[i].answer, 'has-background-danger': result.a !== data[i].answer }"
            >
              Your answer: {{ result.a }}
            </p>
            <p class="has-background-link has-text-white p-2" v-if="result.a !== data[i].answer">Correct answer: {{ data[i].answer }}</p>
          </li>
        </ul>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  props: ['data', 'results'],
  setup(props, context) {
    // On close
    const handleClose = () => {
      context.emit('close')
    }

    return { handleClose }
  }
}
</script>

<style>

</style>