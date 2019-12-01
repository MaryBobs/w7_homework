<template lang="html">
  <div>
    <h2 v-if="answer">{{answer.correct_answer}}</h2>
  </div>

</template>

<script>
export default {
  name: "answer",
  props: ["answer"]
}
</script>

<style lang="css" scoped>
</style>
