<template lang="html">
  <div>
  <h2>Quiz</h2>
  <question-list :questions="questions"></question-list>
  <result :result="this.finalResult"></result>
</div>
</template>

<script>
import QuestionList from "./components/QuestionList.vue"
import Result from "./components/Answer.vue"
import {eventBus} from "./main.js"

export default {
  name: "app",
  data(){
    return {
    questions: [],
    selectedQuestion: null,
    finalResult: null
    }
  },
  mounted(){
    fetch("https://opentdb.com/api.php?amount=5&type=boolean&encode=url3986")
    .then(res => res.json())
    .then(data => this.questions = data.results)

    eventBus.$on("question-picked", payload => {
      this.selectedQuestion = payload;

      eventBus.$on("the-result", payload => {
        this.finalResult = payload;
      })
    })
  },
  components: {
    "question-list": QuestionList,
    "result": Result,
  }
}
</script>

<style lang="css" scoped>
</style>
