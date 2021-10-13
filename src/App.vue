<template>
  <div class="ctr">
    <transition name="fade" mode="out-in">
      <questions
          v-if="questionsAnswered < questions.length"
          :questions="questions"
          :questionsAnswered="questionsAnswered"
          @question-answered="questionAnswered"
      />
      <result
          v-else
          :results="results"
          :totalCorrect="totalCorrect"
      />
    </transition>

    <button type="button" class="reset-btn"
            @click.prevent="reset"
            v-show="questionsAnswered === questions.length"
    >Reset
    </button>
  </div>
</template>

<script>
import Questions from "./components/Questions";
import Result from "./components/Result";

export default {
  name: 'App',
  components: {
    Questions,
    Result
  },
  data() {
    return {
      questionsAnswered: 0,
      totalCorrect: 0,
      questions: [
        {
          q: 'The knowledge that the earth is not flat has been known for thousands of years.',
          answers: [
            {
              text: 'True',
              is_correct: true
            },
            {
              text: 'False',
              is_correct: false
            }
          ]
        },
        {
          q: 'What is the oldest federal republic still in existence?',
          answers: [
            {
              text: 'Germany',
              is_correct: false
            },
            {
              text: 'United Kingdom',
              is_correct: false
            },
            {
              text: 'United States',
              is_correct: true
            },
            {
              text: 'Spain',
              is_correct: false
            }
          ]
        },
        {
          q: 'In which country was the pacemaker invented?',
          answers: [
            {
              text: 'United States',
              is_correct: false
            },
            {
              text: 'Canada',
              is_correct: true
            },
            {
              text: 'Colombia',
              is_correct: true
            },
            {
              text: 'Australia',
              is_correct: false
            },
          ]
        },
      ],
      results: [
        {
          min: 0,
          max: 2,
          title: "Try again!",
          desc: "Do a little more studying and you may succeed!"
        },
        {
          min: 3,
          max: 3,
          title: "Wow, you're a genius!",
          desc: "Studying has definitely paid off for you!"
        }
      ]
    }
  },
  methods: {
    questionAnswered(answer) {
      if (answer) this.totalCorrect++
      this.questionsAnswered++
    },
    reset() {
      this.questionsAnswered = 0
      this.totalCorrect = 0
    }
  }
}
</script>

<style>
</style>
