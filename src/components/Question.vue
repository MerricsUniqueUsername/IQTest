<template>
  <div>
    <div v-if="isLoading" class="loading-container">
      <div class="loading-spinner"></div>
    </div>
    <template v-else>
      <h1 class="question">{{ question }}</h1>
      <div class="horizontal-line"></div>
      <div class="answers">
        <Answer 
          class="answer" 
          @click="$emit('postAnswer', answer)" 
          v-for="answer in answers" 
          :key="answer" 
          :text="answer"
          v-show="!String(answer).includes('depend')"
        />
      </div>
    </template>
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
  computed: {
    isLoading() {
      return !this.question && (!this.answers || this.answers.length === 0);
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
  font-size: 25px;
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

/* Loading spinner styles */
.loading-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 200px;
}

.loading-spinner {
  width: 50px;
  height: 50px;
  border: 3px solid #f3f3f3;
  border-top: 3px solid #3498db;
  border-radius: 50%;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}
</style>