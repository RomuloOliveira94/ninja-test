<template>
  <p>Reaction time: {{ score }}ms</p>
  <p>{{ rank }}</p>
  <button @click="$emit('retry')">Retry</button>
</template>

<script>
export default {
  emits: ["retry"],
  props: ["score"],
  data() {
    return {
      rank: null,
    };
  },
  mounted() {
    if (this.score < 250) {
      this.rank = "Ninja!";
    }
    if (this.score < 400) {
      this.rank = "Good Reflexes";
    } else {
      this.rank = "Try Again!";
    }
  },
};
</script>

<style>
</style>