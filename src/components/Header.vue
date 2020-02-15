<template>
    <div>
        <h1>Tech Quiz</h1>
        <b-nav>
            <b-nav-item disabled>Score: {{numOfCorrectAns}}/{{numTotal}}</b-nav-item>
            <b-nav-item disabled>Question: {{questionNumber + 1 }}/10</b-nav-item>
        </b-nav>
    </div>
</template>
<script>
export default {
   props:[
       "numOfCorrectAns",
       "numTotal",
       "questionNumber"
   ] 
}
</script>
<style scoped>
.nav{
 justify-content: center;
}
  
</style>