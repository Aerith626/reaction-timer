<template>
  <div v-if="showBlock"  @click="reaction(); $emit('togglePlay', reactionTime)" class="block block__overlay block__play">
    <h3>{{text}}</h3>
  </div>
  
</template>
  
  
<script setup>

import {onMounted, ref} from 'vue'



const props = defineProps({
  text: {
    type: String,
    default: 'Click me'
  },
  delay: {
    type: Number
  }
})

const emits = defineEmits([
  'togglePlay'
])

/* Data */
const showBlock = ref(false);
const reactionTime = ref(0) 
const timeStart = Date.now() + props.delay


/* Methods */


const reaction = () => {
  showBlock.value = false;
  const timeStop = Date.now() - timeStart
  reactionTime.value = timeStop;
}


/* On Mounted */
onMounted(()=>{
  setTimeout( () => {
    showBlock.value = true;
  }, props.delay)
  
})

</script>
  
<style>
  .block__play {
    
  }
</style>
  