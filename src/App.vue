<template>

  <main>
    <h1>Reaction time test</h1>

    <div class="block block__inactive"  @click.self="start">
      <h3 @click="start">{{ !playing ? 'Click to start': 'Wait...'}}</h3>
      <span class="text__span" v-if="fast">Too fast! try again</span>
      <p @click="start" v-if="result.length == 0 && !playing">When you start the game, wait for the background to turn green, then click it as fast as you can</p>
      <Block v-if="playing"  :playing="playing" :delay="delay" @togglePlay="togglePlaying" text="Click!" />
      <Results @click="start" :average="avg" :length="result" :results="(result.slice(-1))[0]" v-if="!playing && result.length > 0 && !fast" />
    </div>

    <div v-if="result.length > 0" class="list">
      <h4>Results</h4>
      <ul>
        <li v-for="score in result">{{score}}ms</li>
      </ul>
      
    </div>
    
  </main>

</template>


<script setup>
/* Imports */
import {ref} from 'vue'
import Block from './components/Block.vue'
import Results from './components/Results.vue'


/* Data */
const playing = ref(false)
const delay = ref(null) 
const result = ref([])
const fast = ref(false)
const avg = ref(null)
const blockResult = ref(null)




/* Methods */
const start = () => {
  if(playing.value == false) {
    fast.value = false
    playing.value = true
    delay.value = 800 + Math.random()*3500
  } else {
    playing.value = false
    fast.value = true
  }
}

const togglePlaying = (reactionTime) => {
  playing.value = false
  result.value.push(Math.trunc(reactionTime))
  blockResult.value = reactionTime
  avg.value = Math.trunc(result.value.reduce((a, b) => a + b, 0)/result.value.length)
}

/* Si showBlock = false y playing = true, reset */
</script>

<style>


  </style>
