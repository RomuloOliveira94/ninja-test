<script>
import Block from "./components/Block.vue";
import Results from "./components/Results.vue";
export default {
  name: "app",
  components: { Block, Results },
  data() {
    return {
      isPlaying: false,
      delay: null,
      score: null,
      showResult: false,
    };
  },
  methods: {
    start() {
      this.delay = 2000 + Math.random() * 5000;
      this.isPlaying = true;
    },
    endGame(reactionTime) {
      this.score = reactionTime;
      this.showResult = true;
    },
    retrying(){
      this.showResult = false;
      this.isPlaying = false;
    }
  },
};
</script>

<template>
  <h1>Reaction Timer</h1>
  <button @click="start" :disabled="isPlaying">Play</button>
  <Results :score="score" v-if="showResult" @retry="retrying"/>
  <Block v-if="isPlaying" :delay="delay" @end="endGame" />
</template>

<style>
@import "./assets/base.css";

#app {
  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;
  font-weight: normal;
}

header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

a,
.green {
  text-decoration: none;
  color: hsla(160, 100%, 37%, 1);
  transition: 0.4s;
}
</style>
