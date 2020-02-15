<template>
<div>
    <h2 v-if="score >= 6">Congratulations!!</h2>
    <h2 v-if="score >= 4 && score < 6">Satisfactory Result!</h2>
    <h2 v-if="score < 4">Extremely Poor!</h2>
    <h4>You Scored {{score}} out of 10</h4>
     <b-button variant="success" @click="restart">More Quiz!!</b-button>
    </div>
   
</template>
<script>
export default {
    props:{
        score: Number,
        restart: Function
    }
}
</script>
