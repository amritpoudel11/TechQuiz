<template>
  <div id="app">
    <Header :numOfCorrectAns="numOfCorrectAns" :numTotal="numTotal" :questionNumber="index"/>
    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="12" md="8" lg="6" offset-sm="0" offset-md="2" offset-lg="3">
          <QuestionBox v-if="!last && questions.length" :currQuestion="questions[index]" :next="next" :increment="increment" :last="last"/>
          <ResultBox v-if="last" :score="numOfCorrectAns" :restart="restart"/>
        </b-col>
      </b-row>
    </b-container>
    <Footer/>
  </div>
  
</template>

<script>
import Header from "./components/Header.vue";
import QuestionBox from "./components/QuestionBox.vue";
import ResultBox from "./components/ResultBox.vue";
import Footer from "./components/Footer.vue";

export default {
  name: "app",
  components: {
    Header,
    QuestionBox,
    ResultBox,
    Footer
  },
  data() {
    return {
      questions: [],
      index: 0,
      numOfCorrectAns: 0,
      numTotal: 0,
      last: false
    };
  },
  methods: {
    next() {
      if(this.index < 9){
        this.index++;
      }else{
        this.last = true;
      }
    },
    increment(isCorrect){
      if(isCorrect){
        this.numOfCorrectAns++;
      }
      this.numTotal++;
    },
    restart(){
      this.questions = [];
      this.index = 0;
      this.numOfCorrectAns = 0;
      this.numTotal = 0;
      this.last = false;
      this.getQuestions();
    },
    getQuestions(){
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
  font-family:'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #d0dae4;
  padding-top: 2vh;
  background-color: rgba(54, 47, 47, 0.7) !important;
  
}
body{
 background-color: rgba(54, 47, 47, 0.7) !important;

}
</style>
