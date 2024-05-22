<script setup lang='ts'>
import {  computed, ref } from 'vue';
import { Player } from '../models/Player';


const playingField = ref([
    {text:""},{text:""},{text:""},
    {text:""},{text:""},{text:""},
    {text:""},{text:""},{text:""}
])
      
interface Square {
  text: string;
}

function calculateWinner(squares: Square[]): string | null{
  const winningCombinations = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  for (let i = 0; i < winningCombinations.length; i++) {
    const [a, b, c] = winningCombinations[i];
    if (squares[a].text && squares[a].text === squares[b].text && squares[a].text === squares[c].text) {
      return squares[a].text;
    }
  }
  return null;
}


const theWinner = computed(() => calculateWinner(playingField.value))

function isTie(): boolean {
    return !theWinner.value && playingField.value.every(square => square.text !== "");
}
 
      interface PlayersProps{
          playersInGame: Player[]
        }
        const props = defineProps<PlayersProps>();
        
        const currentPlayer = ref<Player>(props.playersInGame[0])

function makeMove(i: number) {
    if (playingField.value[i].text !== "") {
        return;
    }
    
    playingField.value[i].text = currentPlayer?.value?.playerSymbol!;

    if (currentPlayer.value === props.playersInGame[0]) {
        currentPlayer.value = props.playersInGame[1]
    }   else{
        currentPlayer.value = props.playersInGame[0]
    }
}
  
function resetGame() {
  playingField.value = [
    { text: "" }, { text: "" }, { text: "" },
    { text: "" }, { text: "" }, { text: "" },
    { text: "" }, { text: "" }, { text: "" }
  ];
  currentPlayer.value = props.playersInGame[0];
}

</script>

<template>
    <h4>Let the game begin</h4>
    <p>spelare X: {{ playersInGame[0].playerName }} & spelare O: {{ playersInGame[1].playerName }}</p>
    <p>Din Tur: {{ currentPlayer?.playerName }}</p>
    <h2 v-if="theWinner"> {{ theWinner}}: vann</h2>
    <h2 v-if="isTie()">Oavgjort</h2>
    <section id="playingField">
    <div @click="makeMove(i)" class="square" v-for="(square, i) in playingField" key="i">{{ square.text }}</div>
    <button @click="resetGame">Nytt spel</button>
    </section>
</template>

<style scoped>
    #playingField{
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        grid-template-rows: repeat(3, 1fr);
        gap: 0.5em;
    }
    .square{
        background-color: aliceblue;  
        border: solid darkblue 2px;
        padding: 1em;
        height: 2em;
        width: 2em;
        }
</style>