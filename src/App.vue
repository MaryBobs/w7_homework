<template lang="html">
  <div>
  <h2>Quiz</h2>
  <question-list :questions="questions"></question-list>
  <answer :answer="this.selectedQuestion"></answer>
</div>
</template>

<script>
import QuestionList from "./components/QuestionList.vue"
import Answer from "./components/Answer.vue"
import {eventBus} from "./main.js"

export default {
  name: "app",
  data(){
    return {
    questions: [],
    selectedQuestion: null,
    selectedAnswer: null
    }
  },
  mounted(){
    fetch("https://opentdb.com/api.php?amount=10&type=boolean&encode=url3986")
    .then(res => res.json())
    .then(data => this.questions = data.results)

    eventBus.$on("question-picked", payload => {
      this.selectedQuestion = payload;

      eventBus.$on("answer-selected", payload => {
        this.selectedAnswer = payload;
      })
    })
  },
  components: {
    "question-list": QuestionList,
    "answer": Answer
  }
}
</script>

<style lang="css" scoped>
</style>
