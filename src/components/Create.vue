<template lang="html">
  <div>
  <h2>Create your Quiz!!</h2>
  <form v-on:submit.prevent="emitCreateQuiz">
    <label for="num-of-questions">Number of questions:</label>
    <input v-model="quiz.number" type="number" name="num-of-questions" min="1" max="10" required>
    <label for="category">Category:</label>
    <select v-model="quiz.category" required>
      <option value="0">Pot Luck! (selects from all categories)</option>
      <option v-for="(category) in categories" :value="category.id">{{category.name}}</option>
      </select>
      <input type="submit" value="Create Quiz">
  </form>
  <h5>Please Note: if your quiz does not generate it may be because there are not enough questions available in
  your chosen category. Try reducing the number of questions or select a different category</h5>
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
