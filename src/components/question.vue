<template lang="html">
<li>
<h2>{{decodeURIComponent(question.question)}}</h2>
</li>
</template>

<script>
export default {
  name:"question",
  props: ["question"],
  methods:{

  }
}
</script>

<style lang="css" scoped>
</style>
