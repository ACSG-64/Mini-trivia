<template>
  <div class="result">
    <div class="title">
      {{ results[resultIndex].title }}
    </div>
    <div class="desc">
      {{ results[resultIndex].desc }}
    </div>
  </div>
</template>

<script>
export default {
  name: "Result",
  props: {
    results: Array,
    totalCorrect: Number
  },
  computed: {
    resultIndex() {
      let index = 0

      this.results.forEach((result, i) => {
        if (this.totalCorrect >= result.min &&
            this.totalCorrect <= result.max) {
          index = i
        }
      })

      return index
    }
  }
}
</script>
