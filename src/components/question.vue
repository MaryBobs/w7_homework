<template lang="html">
<li>
<form v-on:submit.prevent="emitChosenAnswer">
  <h3>{{decodeURIComponent(question.question)}}</h3>
  <input type="radio" v-model="selectedAnswer" value="True">True
  <input type="radio" v-model="selectedAnswer" value="False">False
<input v-on:click="handleClick" type="submit" value="submit">
</form>
</li>
</template>

<script>
import {eventBus} from "../main.js"

export default {
  name: "question",
  props: ["question"],
  computed: {
    finalResult: function(){
      return this.question.correct_answer === this.selectedAnswer ? "correct" : "incorrect";
    }
  },
  data(){
    return {
      selectedAnswer: null
    }
  },
  methods:{
    handleClick(){
      eventBus.$emit("question-picked", this.question);
    },

    emitChosenAnswer(){
      eventBus.$emit("the-result", this.finalResult)
    }
  },
}
</script>

<style lang="css" scoped>
.correct {
  background-color: green;
}

.incorrect  {
  color: red;
}
</style>
