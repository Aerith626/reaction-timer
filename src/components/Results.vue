<template>

    <div class="block block__overlay block__result">
      <h2>{{results}} ms</h2>
      <span class="text__span">Click to keep playing!</span>
      <h4 v-if="length.length > 1" >Average ms: <span class="bold__span">{{average}}ms</span></h4>
    </div>
  
  </template>
  
  
  <script setup>
  
  const props = defineProps({
    results:{
      type: Number
    },
    average: {
      type: Number
    },
    length: {
      type: Array
    }
  })
  </script>
  
  <style>
  

  
  </style>
  