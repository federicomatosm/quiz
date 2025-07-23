<template>
    <div class="result" v-if="true">
        <div class="title">{{results[resultIndex].title}}</div>
        <div class="desc">
            {{results[resultIndex].desc}}
        </div>
    </div>
</template>

<script>
export default {
  name: 'Results',
  props: {
    results: {
      type: Array,
      required: true
    },
    totalCorrect: {
      type: Number,
      default: 0
    }
  },
  computed: { 
    resultIndex() {
        let index = 0;

        this.results.forEach((result, i) => {
            if (result.min <= this.totalCorrect && result.max >= this.totalCorrect) {
                index = i;
            }
        });
      return index;
    }
  },
}
</script>