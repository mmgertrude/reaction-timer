<template>
  <h1>Ninja Reaction Timer</h1>
  <!-- disable the button while isplaying is true -->
  <button @click="startGame" :disabled="isPlaying">play</button>
  <Block v-if="isPlaying" :delay="delay" @endOfGame="endGame"/>
  <Results v-if="showResults" :score="score"/>

  
</template>

<script>
//import child components:
import Block from "./components/Block.vue"
import Results from "./components/Results.vue"

export default {
  name: 'App',
  components: { Block, Results},
  data(){
    return{ 
    isPlaying: false,
    delay: null, //time before the block appears
    score: null,
    showResults: false
    }
  },
  methods: {
    startGame(){
      //keep track if user is playing
      //time before the clickable block appears
      //Math.random() gives random number between 0 and 1 eg 0.627
      //  7000 <= milliseconds >= 2000 
      this.delay = 2000 + Math.random() * 5000 
      this.isPlaying = true
      this.showResults = false
    },
     endGame(reactionTime){
       this.score = reactionTime,
       this.isPlaying = false,
       this.showResults = true
     }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color:#444; 
  margin-top: 60px;
}
button {
  background: #0faf87;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  font-size: 16px;
  letter-spacing: 1px;
  cursor: pointer;
  margin: 10px;
}

button[disabled]{
  opacity: 0.2;
  cursor: not-allowed;
}
</style>
