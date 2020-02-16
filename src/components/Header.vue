<template>
    <div class="header">
        <h1 class="appName">Tech Quiz</h1>
        <b-nav>
            <b-nav-item disabled> <h4> Score: {{numOfCorrectAns}}/{{numTotal}}</h4></b-nav-item>
            <b-nav-item disabled> <h4> Question: {{questionNumber + 1 }}/10 </h4></b-nav-item>
            
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
.appName{
    color: bisque; 
}
.header{
    height: 18vh;
    background-color: rgba(22, 19, 19, 0.9);
    font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
}
  
</style>