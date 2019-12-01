<template lang="html">
<li>
<h2 v-on:click="handleClick">{{decodeURIComponent(question.question)}}</h2>
<form v-on:submit.prevent="emitChosenAnswer">
  <input type="radio" v-model="selectedAnswer" value="true">True
  <input type="radio" v-model="selectedAnswer" value="false">False
<input type="submit" value="submit">
</form>

</li>
</template>

<script>
import {eventBus} from "../main.js"

export default {
  name: "question",
  props: ["question"],
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
      eventBus.$emit("answer-selected", this.selectedAnswer)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
