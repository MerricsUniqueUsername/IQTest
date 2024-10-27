<template>
  <div class="quiz">
    <div class="top">
      <div class="question-num">
        {{ questionNum + 1 }}/{{ quiz.length }}
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


        // { question: "What's your favorite color?", answers: ["Red", "Blue", "Green"] },
        // { question: "Who won the Nobel Prize in Literature in 2020?", answers: ["Jane Austen", "George Orwell", "F. Scott Fitzgerald"] },
        // { question: "What's the capital of France?", answers: ["Paris", "London", "Berlin"] },
        // { question: "What is the largest planet in our solar system?", answers: ["Earth", "Jupiter", "Mars"] },
        // { question: "Who painted the Mona Lisa?", answers: ["Leonardo da Vinci", "Vincent van Gogh", "Pablo Picasso"] },
        // { question: "What is the chemical symbol for water?", answers: ["H2O", "O2", "CO2"] },
        // { question: "How many continents are there on Earth?", answers: ["5", "6", "7"] },
        // { question: "Who wrote 'To Kill a Mockingbird'?", answers: ["Harper Lee", "Mark Twain", "Ernest Hemingway"] },
        // { question: "What is the main ingredient in guacamole?", answers: ["Tomato", "Avocado", "Onion"] },
        // { question: "Which planet is known as the Red Planet?", answers: ["Earth", "Mars", "Venus"] },
        // { question: "What is the smallest country in the world?", answers: ["Monaco", "San Marino", "Vatican City"] },
        // { question: "Who wrote 'The Great Gatsby'?", answers: ["F. Scott Fitzgerald", "Jay Gatsby", "Harper Lee"] },
      ],
    
      questionNum: 0,
      answers: {},
      playing: true,
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
      if (this.questionNum === this.quiz.length - 1) {
        this.endQuiz();
        return;
      }

      this.questionNum++;
    }
  },
  mounted() {
    fetch('https://iqtestbackend.vercel.app/create_question')
    .then(response => {
      if (!response.ok) {
        throw new Error('Network response was not ok ' + response.statusText);
      }
      return response.json(); // Parse the JSON from the response
    })
    .then(data => {
      console.log(data); // Use the data here
    })
    .catch(error => {
      console.error('Error fetching data:', error);
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