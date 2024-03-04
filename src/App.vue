<template>
  <header class="header">
    <nav class="container">
      <div>
        <img src="/logo-ninja.png" alt="logo ninjinha" width="100" />
      </div>
      <div>
        <h1 class="text-header">Você é um ninja?</h1>
      </div>
    </nav>
  </header>
  <main @click="parentClick">
    <div class="container">
      <div v-if="!isPlaying && retry">
        <h4>Teste Ninja! 🥷</h4>
        <button
          class="botao-jogar"
          @click="start"
          :disabled="isPlaying"
          @click.stop
        >
          JOGAR!
        </button>
      </div>
      <div v-if="isPlaying && !showResult">
        <small>Concentre-se...</small>
      </div>
      <Results
        :score="score"
        v-if="showResult"
        @retry="retrying"
        :clickedBefore="clickedBefore"
      />
      <Block v-if="isPlaying" :delay="delay" @end="endGame" @click.stop />
    </div>
  </main>
</template>

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
        clickedBefore: false,
        retry: true,
      };
    },
    methods: {
      start() {
        this.delay = 2000 + Math.random() * 5000;
        this.isPlaying = true;
        this.clickedBefore = false;
        this.retry = false;
      },
      endGame(reactionTime) {
        this.score = reactionTime;
        this.showResult = true;
      },
      retrying() {
        this.showResult = false;
        this.isPlaying = false;
        this.retry = true;
      },
      parentClick() {
        if (this.isPlaying) {
          this.clickedBefore = true;
          this.score = 1000;
          this.showResult = true;
          this.isPlaying = false;
        }
      },
    },
  };
</script>

<style>
  @import "./assets/base.css";
  @import url("https://fonts.googleapis.com/css2?family=PT+Serif:ital,wght@0,400;0,700;1,400;1,700&display=swap");

  #app {
    font-weight: normal;
    font-family: "PT+Serif";
    width: 100%;
  }

  .container {
    max-width: 1280px;
    margin: 0 auto;
    padding: 0 1.5rem;
  }

  nav {
    max-width: 1280px;
    margin: 0 auto;
    line-height: 1.5;
    display: flex;
    gap: 2rem;
    align-items: center;
  }

  header {
    border-bottom: 1px solid #f0efef;
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

  .text-header {
    font-size: 2rem;
    margin: 0;
  }

  main {
    height: 70vh;
    display: flex;
    justify-content: center;
    margin-top: 2rem;
    border-bottom: 1px solid #f0efef;
  }

  button {
    padding: 10px 20px;
    font-size: 1.5rem;
    background-color: black;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    width: 100%;
    max-width: 200px;
  }
  .image-ninja {
    background-image: url("../public/ninja-example.jpg");
    background-repeat: no-repeat, no-repeat;
    background-position: center center;
    background-size: cover;
    height: 350px;
    width: 100%;
  }
  .image-ninja-atual {
    background-image: url("../public/ninja-atual.jpg");
    background-repeat: no-repeat, no-repeat;
    background-position: center center;
    background-size: cover;
    height: 350px;
    width: 100%;
  }

  @media (min-width: 1024px) {
    /* Seus estilos para desktop vão aqui */
    .image-ninja {
      background-image: url("../public/ninja-example.jpg");
      background-repeat: no-repeat, no-repeat;
      background-position: center center;
      background-size: cover;
      height: 300px;
      width: 100%;
      margin: 0 auto;
    }

    p {
      font-size: 1.5rem;
      margin-bottom: 20px;
      margin-top: 20px;
    }

    .text-section {
      display: flex;
      gap: 20px;
      padding: 1.5rem;
    }
  }

  section {
    border-bottom: 1px solid #f0efef;
  }
</style>
