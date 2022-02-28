<template>
  <h1>Hi and welcome</h1>

  <button @click="startGame"> 
    <p>Play the game</p>

  </button>
  <Game v-if="isPlaying"/>
</template>

<script>
import Game from './components/Game.vue'


export default {
  
  components: {
    Game
  },
  data() {
    return{
      isPlaying: false
    }
  },
  methods: {
    startGame() {
      this.isPlaying = true
    }
  }
  
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  button{
    padding: 15px;
    border-radius: 30px;
    color: white;
    border: 2px solid white;
    background: yellowgreen;
    display: block;
    margin: 20px auto;

  }
  p{
    margin: 0;
    font-size: 20px;
  }
}
</style>
