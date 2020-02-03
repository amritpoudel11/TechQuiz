<template>
  <div>
    <b-jumbotron>
      <template v-slot:lead>{{currQuestion.question}}</template>

      <hr class="my-4" />

      <b-list-group>
        <b-list-group-item v-for="answer in answers" :key="answer">{{answer}}</b-list-group-item>
      </b-list-group>
      <b-button variant="primary" href="#">Submit</b-button>
      <b-button variant="success" href="#" @click="next">Next</b-button>
    </b-jumbotron>
  </div>
</template>
<script>
export default {
  props: {
    currQuestion: Object,
    next: Function
  },
  computed: {
    answers() {
      let answers = [...this.currQuestion.incorrect_answers];
      answers.push(this.currQuestion.correct_answer);
      return answers;
    }
  }
};
</script>