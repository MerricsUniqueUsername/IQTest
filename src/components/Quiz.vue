<template>
  <div class="quiz">
    <div class="top">
      <div class="question-num">
        {{ questionNum + 1 }}/{{ questionCount }}
      </div>
      <Timer class="timer" ref="timer" />
    </div>
    <Question v-if="playing" @postAnswer="handleAnswer" :question="quiz[questionNum].question" :answers="quiz[questionNum].answers" />
    <EndScreen ref="endscreen" v-if="!playing" :answers="answers" />
  </div>

  <Popup ref="popup"/>
</template>

<script>
import Question from "./Question.vue"
import EndScreen from "./EndScreen.vue"
import Timer from "./Timer.vue"
import Popup from './Popup.vue'
import axios from 'axios'

export default {
  name: "Quiz",
  components: {
    Question,
    EndScreen,
    Timer,
    Popup,
  },
  data() {
    return {
      // Quiz
      quiz: [
        { question: "", answers: [] } 
      ],
    
      questionNum: 0,
      answers: {},
      lastTenAnswers: [],
      playing: true,
      questionCount: 35,
      phase: 1,

      popupNums: [],
      popupIndex: 0,
      popups: null
    }
  },
  methods: {
    endQuiz() {
      this.playing = false;
      this.$refs.timer.stop();

      this.$nextTick(() => {
        if(this.$refs.endscreen) {
          this.$refs.endscreen.calculateIq();
        }
      });
    },
    updatePhase() {
      if(this.questionNum === 5) {
        this.phase = 2;
      }
      if(this.questionNum === 11) {
        this.phase = 3;
      }
      else if(this.questionNum === 17) {
        this.phase = 4;
      }
      else if(this.questionNum === 24) {
        this.phase = 5;
      }
      else if(this.questionNum === 32) {
        this.phase = 6;
      }
    },
    handleAnswer(answer) {
      // Add answer
      this.answers[this.quiz[this.questionNum].question] = answer;

      // Update lastTenAnswers
      this.lastTenAnswers.push({ question: this.quiz[this.questionNum].question, answer: answer });
      if (this.lastTenAnswers.length > 10) {
        this.lastTenAnswers.shift();
      }

      // If final question, stop test
      if (this.questionNum === this.questionCount - 1) {
        this.endQuiz();
        return;
      }

      // Show popup
      this.showPopup();

      this.updatePhase();

      this.questionNum++;
      this.generateQuestion();
    },
    showPopup() {
      if(this.popupNums.includes(this.questionNum))
      this.$refs.popup.showPopup(this.popups[this.popupIndex++]);
    },
    generateQuestion() {

      // Pure logic questions
      if(this.phase == 1) {
        axios.post('https://iqtestbackend.vercel.app/create_question/', {
            currentAnswers: this.answers
        })
        .then(response => {
            this.quiz[this.questionNum] = response.data;
            this.quiz.push({ question: "", answers: [] });
        })
        .catch(error => {
            console.error(error);
            // Try again
            this.generateQuestion();
        });
      }

      // Looking for bias
      else if(this.phase == 2) {
        axios.post('https://iqtestbackend.vercel.app/phase_2/', {
            currentAnswers: this.answers
        })
        .then(response => {
            this.quiz[this.questionNum] = response.data;
            this.quiz.push({ question: "", answers: [] });
        })
        .catch(error => {
            console.error(error);
            // Try again
            this.generateQuestion();
        });
      }

      // Start generating contradictions and getting political
      else if(this.phase == 3) {
        axios.post('https://iqtestbackend.vercel.app/phase_3/', {
            currentAnswers: this.answers
        })
        .then(response => {
            this.quiz[this.questionNum] = response.data;
            this.quiz.push({ question: "", answers: [] });
        })
        .catch(error => {
            console.error(error);
            // Try again
            this.generateQuestion();
        });
        
      }

      // Start challenging the user's opinions
      else if(this.phase == 4) {
        axios.post('https://iqtestbackend.vercel.app/phase_4/', {
            currentAnswers: this.answers
        })
        .then(response => {
            this.quiz[this.questionNum] = response.data;
            this.quiz.push({ question: "", answers: [] });
        })
        .catch(error => {
            console.error(error);
            // Try again
            this.generateQuestion();
        });
      }

      // Very rude
      else if(this.phase == 5) {
        axios.post('https://iqtestbackend.vercel.app/phase_5/', {
            currentAnswers: this.answers
        })
        .then(response => {
            this.quiz[this.questionNum] = response.data;
            this.quiz.push({ question: "", answers: [] });
        })
        .catch(error => {
            console.error(error);
            // Try again
            this.generateQuestion();
        });
      }

      // Full on asshole
      else if(this.phase == 6) {
        axios.post('https://iqtestbackend.vercel.app/phase_6/', {
            currentAnswers: this.answers
        })
        .then(response => {
            this.quiz[this.questionNum] = response.data;
            this.quiz.push({ question: "", answers: [] });
        })
        .catch(error => {
            console.error(error);
            // Try again
            this.generateQuestion();
        });
      }
    }
  },
  mounted() {
    this.generateQuestion();

    // Create popups
    for(let i = 0; i < 3; i++) {
      this.popupNums.push(Math.floor(Math.random() * (24 - 12 + 1)) + 12);
    }

    // Get popups axios
    axios.get('https://iqtestbackend.vercel.app/get_popups/')
     .then(response => {
        this.popups = response.data;      
      })
     .catch(error => {
        console.error(error);
      });
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