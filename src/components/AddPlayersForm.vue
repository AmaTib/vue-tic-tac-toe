<script setup lang="ts">
import { ref } from 'vue';
import { Player } from '../models/Player';


const userInput = ref("")

const players = ref<Player[]>([])

function setPlayer(){
  if (players.value.length  < 2) {
    players.value.push(new Player(userInput.value))
    userInput.value = "" 
    players.value[1].playerX = !players.value[1].playerX;
    
    console.log(players.value);
    
  } else{
    alert("Kan inte vara fler än 2 spelare")
  }
}

defineEmits<{
  (e: "changeView", arrLength:number): void;
}>();

</script>

<template>
  <h1>Skapa spelare</h1>
  <form @submit.prevent="setPlayer">
    <input type="text"  v-model="userInput"/>
    <button v-if="players.length === 0">Lägg till spelare x</button>
    <button v-else>Lägg till spelare o</button>

  </form>
  <ul>
    <li v-for="(player, i) in players" :key="i">
      <p v-if="player.playerX">Spelare X:</p>
      <p v-else>Spelare O:</p>
    {{ player.playerName }}</li>
  </ul>

<button @click="$emit('changeView', players.length)">spela</button>

</template>

<style scoped></style>
