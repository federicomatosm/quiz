<template>
         <div class="questions-ctr">
          <div class="progress">
              <div class="bar" :style="{width: `${(questionsAnswered / questions.length)*100}%`}"></div>
              <div class="status">{{questionsAnswered}} out of {{questions.length}} questions answered</div>
          </div>
          <transition-group name="fade">
          <div class="single-question" 
          v-for="(question, index) in questions" 
          :key="index"
          v-show="index === questionsAnswered"
          >
              <div class="question">{{question.q}}</div>
              <div class="answers" >
                  <div class="answer" 
                  v-for="(answer, answerIndex) in question.answers" 
                  :key="answerIndex"
                  @click.prevent="selectAnswer(answer.is_correct, index)"
                  >
                  {{answer.text}}
                </div>                  
              </div>
          </div>
          </transition-group>
      </div>
</template>

<script>
export default {
  name: 'Questions',
  props: {
    questions: {
      type: Array,
      required: true
    },
    questionsAnswered: {
      type: Number,
      default: 0
    }
  },
  emits: ['question-aswered'],
  methods: {
    selectAnswer(isCorrect, index) {
      if (isCorrect) {
        console.log('Correct answer!');
      } else {
        console.log('Wrong answer!');
      }
      this.$emit('question-aswered', isCorrect, index);
    }
  }

}
</script>