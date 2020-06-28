<template>
  <div>
    <div id="app">
      <div id="details">
        <div class="scoredBoard">
          <span> O победил {{ wins.O }} раз</span>
          <span> Х победил {{ wins.X }} раз</span>
        </div>
        <h1>Krestiki-Noliki</h1>
        <h2>Match #{{ matches + 1 }}</h2>
      </div>
      <grid></grid>
      <button class="restart"
              @click="restart">Restart</button>
    </div>
  </div>
</template>

<script>
import Grid from './components/Grid.vue'

export default {
  components: { Grid },
  name: 'app',

  data () {
    return {
      matches: 0,
      wins: {
        O: 0,
        X: 0
      }
    }
  },

  methods: {
    restart () {
      Event.$emit('clearCell')
      Event.$emit('gridReset')
      this.matches++
    }
  },

  created () {
    Event.$on('win', winner => this.wins[winner]++)
  }
}
</script>

<style>
body {
  background-color: #fff;
  color: #fff;
  font-family: 'Dosis', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin: 0px auto;
  width: 100%;
  max-width: 270px;
}
#app {
  margin: 0 auto;
  max-width: 270px;
  color: #34495e;
}
h1 {
  text-transform: uppercase;
  font-weight: bold;
  font-size: 3em;
}
.restart {
  background-color: #e74c3c;
  color: #fff;
  border: 0px;
  border-bottom-left-radius: 10px;
  border-bottom-right-radius: 10px;
  font-family: 'Dosis', sans-serif;
  font-size: 1.4em;
  font-weight: bold;
  margin: 0px;
  padding: 15px;
  width: 100%;
}
.restart:hover {
  background-color: #c0392b;
  cursor: pointer;
}
.scoredBoard {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;
  height: 60px;
  background-color: #16a085;
  box-shadow: 10px solid #fff;
  padding: 20px;
  overflow-x: none;
  max-width: 270px;
}
.scoredBoard h2 {
  margin: 0px;
}
.scoredBoard span {
  float: right;
  font-size: 1.2em;
  font-weight: bold;
  margin-left: 10px;
}
</style>
