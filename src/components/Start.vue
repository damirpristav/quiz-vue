<template>
  <div class="card">
    <div class="card-content">
      <div class="content">
        <h1>Start the quiz</h1>
        <p>Good luck!</p>
        <button class="button is-info is-medium" @click="handleStart">Start</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  setup(props, context) {
    // On start button click
    const handleStart = () => {
      context.emit('startQuiz')
    }

    return { handleStart }
  }
}
</script>

<style>

</style>