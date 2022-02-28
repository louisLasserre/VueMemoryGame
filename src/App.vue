<template>
    <h1>Hi and welcome</h1>

    <button @click="startGame" v-if="!isPlaying">
        <p>Play the game</p>

    </button>
    <h3 v-if="!isPlaying">Nombre de cartes</h3>
    <div class="flex" v-if="!isPlaying">
        <input placeholder="entrez un nombre paire positif" size="30" type="text" v-model="nbrCards"><p>{{ nbrCards }}</p>
        {{ erreur }}
    </div>


    <Game :nbrCards="nbrCards" @win="showWin" v-if="isPlaying"/>
    <p v-if="win">you won</p>
</template>

<script>
import Game from './components/Game.vue'


export default {
  
  components: {
    Game
  },
  data() {
    return{
      isPlaying: false,
      win: false,
      nbrCards: null,
      erreur: null
    }
  },
  methods: {
    startGame() {
      if(this.nbrCards == null || this.nbrCards == ""){
        this.erreur = "you must enter a number"
      }else{
        
        if(!isNaN(parseInt(this.nbrCards)) && !isNaN(this.nbrCards - 0) == true){
          if(this.nbrCards = parseInt(this.nbrCards)){
            
            if(this.nbrCards > 0 && this.nbrCards < 30){
              if(this.nbrCards % 2 == 0){

                console.log(this.nbrCards)
                this.win = false
                this.isPlaying = true

              }else{
                this.erreur = "please enter an even number"
              }

            }else{
              this.erreur = "enter a number situated between 0 and 30"
            }
          }else{
            this.erreur = "you must enter a valid number"
          }

        }else{
          this.erreur = "you must enter a number"
        }

        
        
      }
      


    },
    showWin(){
      this.isPlaying = false
      this.win = true
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
        button {
            padding: 15px;
            border-radius: 30px;
            color: white;
            border: 2px solid white;
            background: yellowgreen;
            display: block;
            margin: 20px auto;

        }
        p {
            margin: 0;
            font-size: 20px;
        }
        .flex {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            button {
                margin: 0 10px;
                padding: 10px;
            }
        }
    }
</style>
