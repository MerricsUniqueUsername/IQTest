<template>
  <div class="quiz">
    <div class="top">
      <div class="question-num">
        {{ questionNum + 1 }}/{{ questionCount }}
      </div>
      <Timer class="timer" ref="timer" />
    </div>
    <Question v-if="playing" @postAnswer="handleAnswer" :question="quiz[questionNum].question" :answers="quiz[questionNum].answers" />
    <EndScreen v-if="!playing" :answers="answers" />
  </div>
</template>

<script>
import Question from "./Question.vue"
import EndScreen from "./EndScreen.vue"
import Timer from "./Timer.vue"
import axios from 'axios'

export default {
  name: "Quiz",
  components: {
    Question,
    EndScreen,
    Timer,
  },
  data() {
    return {

      // Quiz
      quiz: [
        { question: "", answers: [] } 
      ],
    
      questionNum: 0,
      answers: {},
      playing: true,
      questionCount: 10,
    }
  },
  methods: {
    endQuiz() {
      this.playing = false;
      this.$refs.timer.stop();
    },
    handleAnswer(answer) {

      // Add answer
      this.answers[this.quiz[this.questionNum].question] = answer;

      // If final question, stop test
      if (this.questionNum === this.questionCount - 1) {
        this.endQuiz();
        return;
      }

      this.questionNum++;
      this.generateQuestion();
    },
    generateQuestion() {
      axios.get('https://iqtestbackend.vercel.app/create_question')
      .then(response => {
        this.quiz[this.questionNum] = response.data
        this.quiz.push({ question: "", answers: [] } )
      })
      .catch(error => {
        console.error(error);
      });
    }
  },
  mounted() {
    this.generateQuestion();
  }
}
</script>

<style>

.quiz {
  justify-content: center;
  border: rgb(207, 207, 207) solid 1px;
  border-radius: 3px;
  margin: 30px;
  min-height: 80vh;
}

.top {
  display: flex;
  width: 100%;
  justify-content: space-between;
  font-size: 2rem;
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
  border-bottom: rgb(207, 207, 207) solid 1px;
  box-shadow: 0 2px 40px 0 rgba(0, 0, 0, 0.1);
}
.timer {
  margin-right: 10px;
}
.question-num {
  margin-left: 10px;
}

</style>