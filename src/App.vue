<template lang="html">
  <div id="app">
    <h1>Quiz Generator</h1>
    <create :categories="categories"></create>
  <div class="q-list">
  <question-list :questions="questions"></question-list>
  <div class="result">
  <result :result="finalResult"></result>
  </div>
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
    }
  }

}
</script>

<style lang="css" >
  * {
    margin-top: 0px;
    background-color: #454B66;
    font-family: 'Roboto Mono', monospace;
    font-weight: lighter;
    color: #DCDCDD;
    font-size: 20px;
  }
  h1  {
    font-size: 35px;
    align-self: center;
    font-weight: normal;
  }
  h2  {
    font-size: 38px;
  }
  li {
    list-style: none;
    padding: 5px;
    border: solid 2px;
    border-color: white;
    border-radius: 5px;
    margin: 5px;
  }
  input {
    background-color: white;
    color: #454B66;
  }
  .q-list {
    display: flex;
    justify-content: space-between;
  }
  .result {
    align-content: stretch;
  }
</style>
