<template lang="html">
  <div>
    <h2>Quiz</h2>
    <create :categories="categories"></create>
  <div class="main">
  <question-list :questions="questions"></question-list>
  <result :result="finalResult"></result>
</div>
</div>
</template>

<script>
import QuestionList from "./components/QuestionList.vue"
import Result from "./components/Answer.vue"
import Create from "./components/Create.vue"
import {eventBus} from "./main.js"

export default {
  name: "app",
  data(){
    return {
    questions: [],
    categories: [],
    selectedQuestion: null,
    finalResult: null,
    quizNumberOfQuestions: null,
    quizCategory: null
    }
  },
  mounted(){
    // fetch("https://opentdb.com/api.php?amount=5&type=boolean&encode=url3986")
    // .then(res => res.json())
    // .then(data => this.questions = data.results),

    fetch("https://opentdb.com/api_category.php")
    .then(res => res.json())
    .then(categories => this.categories = categories.trivia_categories)

    eventBus.$on("question-picked", payload => {
      this.selectedQuestion = payload;
})
    eventBus.$on("the-result", payload => {
      this.finalResult = payload;
})
    eventBus.$on("created-quiz", payload => {
      this.quizNumberOfQuestions = payload.number;
      this.quizCategory = payload.category;
      this.fetchNewQuiz(payload);
    })
      },
  components: {
    "question-list": QuestionList,
    "result": Result,
    "create": Create
  },
  methods: {
    fetchNewQuiz: function() {
      const url = `https://opentdb.com/api.php?amount=${this.quizNumberOfQuestions}&category=${this.quizCategory}&type=boolean&encode=url3986`;
      fetch(url)
      .then(res => res.json())
      .then(data => this.questions = data.results)
      console.log(url);
    }
  }

}
</script>

<style lang="css" scoped>
  .main {
    display: flex;
    justify-content: space-between;
  }
</style>
