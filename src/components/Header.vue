<template>
    <div>
        <h1>Computer Science Quiz</h1>
        <b-nav>
            <b-nav-item disabled>Score: {{numOfCorrectAns}}/{{numTotal}}</b-nav-item>
            <b-nav-item disabled>Question: 2/10</b-nav-item>
        </b-nav>
    </div>
</template>
<script>
export default {
   props:[
       "numOfCorrectAns",
       "numTotal"
   ] 
}
</script>
<style scoped>
.nav{
 justify-content: center;
}
  
</style>