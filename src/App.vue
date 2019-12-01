<template lang="html">
  <div>
  <h2>Quiz</h2>
  <question-list :questions="questions"></question-list>
</div>
</template>

<script>
import QuestionList from "./components/QuestionList.vue"

export default {
  name: "app",
  data(){
    return {
    questions: []
    }
  },
  mounted(){
    fetch("https://opentdb.com/api.php?amount=10&type=boolean&encode=url3986")
    .then(res => res.json())
    .then(data => this.questions = data.results)
  },
  components: {
    "question-list": QuestionList
  }
}
</script>

<style lang="css" scoped>
</style>
