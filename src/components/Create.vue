<template lang="html">
  <div>
  <h1>Create your Quiz!!</h1>
  <form v-on:submit.prevent="emitCreateQuiz">
    <label for="num-of-questions">Number of questions:</label>
    <input id="number" v-model="quiz.number" type="number" name="num-of-questions" min="1" max="50">
    <label for="category">Category:</label>
    <select v-model="quiz.category" >
      <option value="0">Select questions from All Categories</option>
      <option v-for="(category) in categories" :value="category.id">{{category.name}}</option>
      </select>
      <input type="submit" value="Create Quiz">
  </form>
    </div>
</template>

<script>
import {eventBus} from "../main.js"

export default {
  name: "create-quiz",
  props: ["categories"],
  data(){
  return {
    quiz: {
      number: null,
      category: null
    }
  }
},
  methods:{
    emitCreateQuiz: function(){
      eventBus.$emit("created-quiz", this.quiz);
    }
}
}
</script>

<style lang="css" scoped>
</style>
