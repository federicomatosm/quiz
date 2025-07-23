<template>
  <div class="ctr">
    <transition name="fade" mode="out-in">
        <questions 
          v-if="questionsAnswered< questions.length" 
          :questions="questions" 
          :questionsAnswered="questionsAnswered"
          @question-aswered="handleQuestionsAnswered"
          />
        <results v-else :results="results" :totalCorrect="totalCorrect"/>
      </transition>

    <button type="button" class="reset-btn" @click.prevent="resetQuiz" v-if="this.questionsAnswered == questions.length">Reset</button>
  </div>
</template>

<script>
import Questions from './components/Questions.vue'
import Results from './components/Results.vue';


export default {
  name: 'App',
  components: {
    Questions,
    Results
  },
  methods: {
    resetQuiz() {
      this.questionsAnswered = 0;
      this.totalCorrect = 0;
      console.log('Quiz has been reset.');
      
    },
    handleQuestionsAnswered(isCorrect, index) {
      this.questionsAnswered++;
      if (isCorrect) {
        this.totalCorrect++;
      } else {
        console.log('Wrong answer!');
      }
      console.log(`Question ${index + 1} answered. Total answered: ${this.questionsAnswered}`);
    }
  },
  data() {
    return {
      questionsAnswered: 0,
      totalCorrect: 0,

      // Sample questions and results
      // In a real application, these would likely be fetched from an API or defined in a separate file
      questions: [
        {
          q: 'What is 2 + 2?',
          answers: [
            {
              text: '4',
              is_correct: true
            },
            {
              text: '3',
              is_correct: false
            },
            {
              text: 'Fish',
              is_correct: false
            },
            {
              text: '5',
              is_correct: false
            }
          ]
        },
        {
          q: 'How many letters are in the word "Banana"?',
          answers: [
            {
              text: '5',
              is_correct: false
            },
            {
              text: '7',
              is_correct: false
            },
            {
              text: '6',
              is_correct: true
            },
            {
              text: '12',
              is_correct: false
            }
          ]
        },
        {
          q: 'Find the missing letter: C_ke',
          answers: [
            {
              text: 'e',
              is_correct: false
            },
            {
              text: 'a',
              is_correct: true
            },
            {
              text: 'i',
              is_correct: false
            }
          ]
        },
      ],
      results: [
        {
          min: 0,
          max: 2,
          title: "Try again!",
          desc: "Do a little more studying and you may succeed!"
        },
        {
          min: 3,
          max: 3,
          title: "Wow, you're a genius!",
          desc: "Studying has definitely paid off for you!"
        }
      ]
    }
  }
}
</script>

<style></style>
