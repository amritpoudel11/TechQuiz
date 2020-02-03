<template>
  <div id="app">
    <Header :numOfCorrectAns="numOfCorrectAns" :numTotal="numTotal"/>
    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">
          <QuestionBox v-if="questions.length" :currQuestion="questions[index]" :next="next" :increment="increment"/>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import QuestionBox from "./components/QuestionBox.vue";

export default {
  name: "app",
  components: {
    Header,
    QuestionBox
  },
  data() {
    return {
      questions: [],
      index: 0,
      numOfCorrectAns: 0,
      numTotal: 0
    };
  },
  methods: {
    next() {
      if(this.index < 10){
        this.index++;
      } 
    },
    increment(isCorrect){
      if(isCorrect){
        this.numOfCorrectAns++;
      }
      this.numTotal++;
    }
  },
  mounted: function() {
    fetch("https://opentdb.com/api.php?amount=10&category=18&type=multiple", {
      method: "get"
    })
      .then(response => {
        return response.json();
      })
      .then(responseJson => {
        this.questions = responseJson.results;
      });
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
body{
  background-color: aquamarine !important;
}
</style>
