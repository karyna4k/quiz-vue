<template>
  <div class="questions-ctr">
    <div class="progress">
      <div
        class="bar"
        :style="{ width: `${getStatusBarWidth}%` }"
      ></div>
      <div class="status">
        {{ questionsAnswered }} out of {{ questions.length }} questions answered
      </div>
    </div>
    <transition-group name="fade">
      <div
        class="single-question"
        v-for="(question, qi) in questions"
        :key="question.q"
        v-show="questionsAnswered === qi"
      >
        <div class="question">{{ question.q }}</div>
        <div
          class="answers"
          v-for="answer in question.answers"
          :key="answer.text"
          @click.prevent="selectAnswer(answer.is_correct)"
        >
          <div class="answer">{{ answer.text }}</div>
        </div>
      </div>
    </transition-group>
  </div>
</template>

<script>
export default {
  props: {
    questions: {
      type: Array,
      required: true,
    },
    questionsAnswered: {
      type: Number,
      required: true,
    },
  },
  emits: ['select-answer'],
  computed: {
    getStatusBarWidth() {
      return (this.questionsAnswered / this.questions.length) * 100;
    },
  },
  methods: {
    selectAnswer(isCorrect) {
      this.$emit('select-answer', isCorrect);
    },
  },
};
</script>
