<template>
  <div class="questions-ctr">
    <div class="progress">
      <div class="bar"
           :style="{ width: `${(questionsAnswered * 100) / questions.length}%`}"></div>
      <div class="status">
        {{ questionsAnswered }} out of {{ questions.length }} questions answered
      </div>
    </div>
    <transition-group name="fade">
      <div class="single-question"
           v-for="(question, q_index) in questions"
           :key="question.q"
           v-show="q_index === questionsAnswered"
      >
        <div class="question">{{ question.q }}</div>
        <div class="answers">
          <div class="answer"
               v-for="answer in question.answers"
               :key="answer.text"
               @click.prevent="selectAnswer(answer.is_correct)"
          >
            {{ answer.text }}
          </div>
        </div>
      </div>
    </transition-group>
  </div>
</template>

<script>
export default {
  name: "Questions",
  props: {
    questions: Array,
    questionsAnswered: Number
  },
  emits: ['question-answered'],
  methods: {
    selectAnswer(answer) {
      this.$emit('question-answered', answer)
    }
  }
}
</script>

