<template>
  <div>
    <h1 class="question">{{ question }}</h1>
    <div class="horizontal-line"></div>
    <div class="answers">
      <Answer class="answer" @click="$emit('postAnswer', answer)" v-for="answer in answers" :key="answer" :text="answer" />
    </div>
  </div>
</template>

<script>
import Answer from "./Answer.vue"

export default {
  components: {
    Answer
  },
  props: {
    question: {
      type: String,
      required: true
    },
    answers: {
      type: Array,
      required: true
    }
  },
  emits: ['postAnswer']
}
</script>

<style scoped>
  * {
    font-family: 'Trebuchet MS', sans-serif;
  }

  .question {
    font-size: 45px;
    text-align: center;
    margin-bottom: 20px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .answers {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    margin-bottom: 20px;
  }

  .answer {
    margin: 10px;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s;
  }

  /* Gradient horizontal line from center */
  .horizontal-line {
    margin: auto;
    margin-bottom: 20px;
    width: 80%;
    height: 2px;
    background: linear-gradient(
      to right,
      transparent 0%,
      #b3b3b3 50%,
      transparent 100%
    );
  }
</style>