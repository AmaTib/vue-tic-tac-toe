<script setup lang="ts">
import { ref } from 'vue';
import { Player } from '../models/Player';


const userInput = ref("")

/* const players = ref<Player[]>([]) */

interface PlayersProps{
  players: Player[]
}

const props = defineProps<PlayersProps>();

function setPlayer(){
  if (props.players.length  < 2) {
    const playerSymbol = props.players.length === 0 ? "X":"O";

    props.players.push(new Player(userInput.value, playerSymbol))
    userInput.value = "" 
    
    console.log(props.players);
    
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
      <p>Spelare {{ players[i].playerSymbol }}:</p>
    {{ player.playerName }}</li>
  </ul>

<button @click="$emit('changeView', players.length)">spela</button>

</template>

<style scoped></style>
