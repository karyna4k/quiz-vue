<template>
  <div class="result">
    <div class="title">{{ results[resultIndex].title }}</div>
    <div class="desc">{{ results[resultIndex].desc }}</div>
  </div>
</template>

<script>
export default {
  props: {
    results: {
      type: Array,
      required: true,
    },
    totalCorrect: {
      type: Number,
      required: true,
    },
  },
  computed: {
    resultIndex() {
      let index = 0;

      this.results.forEach((e, i) => {
        if (e.min <= this.totalCorrect && e.min >= this.results.length) {
          index = i;
        }
      });

      return index;
    },
  },
};
</script>
