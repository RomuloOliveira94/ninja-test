<template>
  <p v-if="clickedBefore === false">Tempo de Reação: {{ score }}ms</p>
  <p>{{ rank }}</p>
  <button @click="$emit('retry')">Tentar Novamente</button>
</template>

<script>
  export default {
    emits: ["retry"],
    props: ["score", "clickedBefore"],
    data() {
      return {
        rank: null,
      };
    },
    mounted() {
      if (this.score < 100) {
        this.rank = "Você é um Ninja Supremo!";
      } else if (this.score < 150) {
        this.rank = "Você é um Ninja!";
      } else if (this.score < 400) {
        this.rank = "Você ja é quase um ninja!";
      } else if (this.score < 500) {
        this.rank = "Bons reflexos!";
      } else if (this.score < 600) {
        this.rank = "Você precisa treinar mais!";
      } else {
        this.rank = "Calma jovem gafanhoto, você consegue!";
      }
    },
  };
</script>

<style>
  p {
    font-size: 1.5rem;
    margin-bottom: 20px;
    margin-top: 20px;
  }
</style>
