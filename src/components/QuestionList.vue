<template lang="html">
  <ul>
    <question v-for="(question, index) in questions" :question="question" :key="index"></question>
  </ul>
</template>

<script>
import Question from "./Question.vue"

export default {
  name: "question-list",
  props: ["questions"],
  components: {
    "question": Question
  }
}
</script>

<style lang="css" scoped>
</style>
