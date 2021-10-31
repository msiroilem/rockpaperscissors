<template>
  <div id="app">
    <div class="flex-row buttons">
      <button
        v-for="choice in playerChoices"
        :disabled="playerChoice"
        class="flex-item"
        :key="choice.id"
        @click="selectChoice(choice)"
      >
        <img :src="choice.image" :alt="choice.label" />
        <h4>{{ choice.label }}</h4>
      </button>
    </div>
    <div class="winner-circle flex-row" v-if="winner">
      <div class="flex-item">
        <h4>Player Chose</h4>
        <img :src="playerChoice.image" :alt="playerChoice.label" />
      </div>
      <div>
        <h4>{{ winner }}</h4>
        <button @click="resetGame">Restart</button>
      </div>
      <div class="flex-item">
        <h4>Computer Chose</h4>
        <img :src="compChoice.image" :alt="compChoice.label" />
      </div>
    </div>
  </div>
</template>

<script>
import choices from './choices'
export default {
  name: 'App',
  components: {},
  data: () => ({
    playerChoices: choices,
    playerChoice: null,
    compChoice: null,
    winner: ''
  }),
  methods: {
    selectChoice(choice) {
      this.playerChoice = choice
      this.compChoice = this.playerChoices[Math.floor(Math.random() * 3)]
      this.checkWinner()
    },
    checkWinner() {
      if (this.playerChoice.value === this.compChoice.value) {
        this.winner = "It's a draw!"
      } else if (this.playerChoice.value === 'paper') {
        if (this.compChoice.value === 'scissor') {
          this.winner = 'Computer Won!'
        } else {
          this.winner = 'Player Won!'
        }
      } else if (this.playerChoice.value === 'scissor') {
        if (this.compChoice.value === 'rock') {
          this.winner = 'Computer Won!'
        } else {
          this.winner = 'Player Won!'
        }
      } else {
        if (this.compChoice.value === 'paper') {
          this.winner = 'Computer Won!'
        } else {
          this.winner = 'Player Won!'
        }
      }
    },
    resetGame() {
      this.playerChoice = null
      this.compChoice = null
      this.winner = ''
    }
  }
}
</script>

<style>
html {
  background-color: #383838;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
  color: #f4f6f9;
}

.flex-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.flex-item {
  padding: 1em;
  max-height: 12em;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  background-color: #303030;
  border-radius: 4px;
  border: 1px solid rgba(255, 255, 255, 0);
  color: #f4f6f9;
}

button {
  border: 0;
  cursor: pointer;
  transition: all 0.3s ease;
}

button:disabled {
  cursor: not-allowed;
}

button:hover:not(:disabled) {
  opacity: 0.8;
  border: 1px solid rgba(255, 255, 255, 0.4);
}

.flex-item img {
  width: 250px;
  max-height: 8em;
  align-content: center;
  object-fit: contain;
}

.winner-circle {
  margin-top: 2em;
  border: 1px solid rgba(255, 255, 255, 0.2);
  padding: 1em;
  border-radius: 4px;
}

.winner-circle button {
  padding: 1em 2em;
  border-radius: 4px;
  border: 0;
  background-color: #ffcc00;
  font-weight: 700;
}

.winner-circle button:hover {
  border: 0;
}
</style>
