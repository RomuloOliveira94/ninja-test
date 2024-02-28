<template>
  <div class="block" v-if="showBlock" @click="stopTimer">
    <img src="shuriken.svg" alt="shuriken">
    Clica!
  </div>
</template>

<script>
  export default {
    props: ["delay"],
    data() {
      return {
        showBlock: false,
        timer: null,
        reactionTime: 0,
      };
    },
    mounted() {
      setTimeout(() => {
        this.showBlock = true;
        this.startTimer();
      }, this.delay);
    },
    methods: {
      startTimer() {
        this.timer = setInterval(() => {
          this.reactionTime += 10;
        }, 10);
      },
      stopTimer() {
        clearInterval(this.timer);
        this.showBlock = false;
        this.$emit("end", this.reactionTime);
      },
    },
  };
</script>

<style>
  .block {
    display: flex;
    gap: 10px;
    width: 200px;
    height: 100px;
    border-radius: 20px;
    background: black;
    color: white;
    text-align: center;
    padding: 20px;
    margin: 40px auto;
  }
</style>

<!--O metodo emit manda uma função para o pai, primeiro ele recebe a função como string pode ser qualquer nome, os dados. -->
