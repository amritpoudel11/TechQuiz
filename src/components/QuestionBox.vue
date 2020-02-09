<template>
  <div>
    <b-jumbotron>
      <template v-slot:lead>{{currQuestion.question}}</template>

      <hr class="my-4" />

      <b-list-group>
        <b-list-group-item
          v-for="(answer, index) in shuffledAnswers"
          :key="index"
          @click="selectAnswer(index)"
          :class="[!hasAnswered && selectedIndex === index ? 'selected' : hasAnswered && correctIndex === index ? 'correct' : hasAnswered && selectedIndex === index && correctIndex !== index ? 'incorrect' : '']"
        >{{answer}}</b-list-group-item>
      </b-list-group>
      <b-button variant="primary" @click="submitAnswer" :disabled="selectedIndex === null || hasAnswered">Submit</b-button>
      <b-button variant="success" @click="next" :disabled="!hasAnswered || last">Next</b-button>
    </b-jumbotron>
  </div>
</template>
<script>
export default {
  props: {
    currQuestion: Object,
    next: Function,
    increment: Function,
    last: Boolean
  },
  data() {
    return {
      selectedIndex: null,
      correctIndex: null,
      shuffledAnswers: [],
      hasAnswered: false
    };
  },
  watch: {
    currQuestion: {
      immediate: true,
      handler() {
        this.selectedIndex = null;
        this.hasAnswered = false;
        this.shuffleAnswers();
      }
    }
  },
  computed: {
    answers() {
      let answers = [...this.currQuestion.incorrect_answers];
      answers.push(this.currQuestion.correct_answer);
      return answers;
    }
  },
  methods: {
    selectAnswer(index) {
      this.selectedIndex = index;
    },
    shuffleAnswers() {
      let answers = [
        ...this.currQuestion.incorrect_answers,
        this.currQuestion.correct_answer
      ];
      for (let i = answers.length - 1; i > 0; i--) {
        let j = Math.floor(Math.random() * (i + 1));
        [answers[i], answers[j]] = [answers[j], answers[i]];
      }
      this.shuffledAnswers = answers;
      this.correctIndex = this.shuffledAnswers.indexOf(this.currQuestion.correct_answer);
    },
    submitAnswer(){
        let isCorrect = false;

        if(this.selectedIndex == this.correctIndex){
            isCorrect = true;
        }
        this.increment(isCorrect);
        this.hasAnswered = true;
    }
  }
};
</script>

<style scoped>
.jumbotron {
  background-color: hotpink;
  color: aliceblue;
}
.list-group {
  margin-bottom: 20px;
  color: hotpink;
}
.list-group-item:hover {
  cursor: pointer;
  background-color: antiquewhite;
}
.correct {
  background-color: #00aa00;
}
.selected {
  background-color: #5555ff !important;
}
.incorrect {
  background-color: #ff1010;
}
.btn {
  margin: 10px 10px;
}
</style>