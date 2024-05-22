<script setup lang="ts">
import { ref } from "vue";
import { Player } from "../models/Player";

const userInput = ref("");

interface PlayersProps {
  players: Player[];
}

const props = defineProps<PlayersProps>();

function setPlayer() {
  if (props.players.length < 2) {
    const playerSymbol = props.players.length === 0 ? "X" : "O";

    props.players.push(new Player(userInput.value, playerSymbol));
    userInput.value = "";

    console.log(props.players);
  } else {
    alert("Kan inte vara fler än 2 spelare");
  }
}

defineEmits<{
  (e: "changeView", arrLength: number): void;
}>();
</script>

<template>
  <h2>Skapa spelare</h2>
  <form @submit.prevent="setPlayer">
    <input type="text" v-model="userInput" />
    <button v-if="players.length === 0">Lägg till spelare x</button>
    <button v-else>Lägg till spelare O</button>
  </form>
  <ul>
    <li v-for="(player, i) in players" :key="i">
      <p>Spelare {{ players[i].playerSymbol }}:</p>
      {{ player.playerName }}
    </li>
  </ul>

  <button @click="$emit('changeView', players.length)">spela</button>
</template>

<style scoped>
h2 {
  margin-bottom: 1em;
}
input {
  background-color: #fdf3e7;
  border-radius: 8px;
  outline: none;
  border: 2px solid #e7ddd1;
  padding: 0.9em;
  margin-bottom: 2em;
  margin-right: 1em;
}
input:focus {
  border: 2px solid #2a38ae;
}

li {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 1em;

  p {
    margin-right: 0.5em;
  }
}
</style>
