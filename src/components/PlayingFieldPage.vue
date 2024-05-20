<script setup lang='ts'>
import { onMounted, ref } from 'vue';
import { Player } from '../models/Player';

let playingField = ref([{text:""},{text:""},{text:""},{text:""},{text:""},{text:""},{text:""},{text:""},{text:""}])

const currentPlayerIndex = ref(0)

interface PlayersProps{
  playersInGame: Player[]
}
const props = defineProps<PlayersProps>();

function makeMove(i:number){
    if (playingField.value[i].text === ""){
        const currentPlayer = props.playersInGame[currentPlayerIndex.value];
        playingField.value[i].text = currentPlayer.playerX ? "X" : "O";
       /*  playingField.value[i].text = "X" */
       currentPlayerIndex.value = currentPlayerIndex.value === 0 ? 1 : 0;
    }
}

</script>

<template>
    <h4>Let the game begin</h4>
    <p>spelare X: {{ playersInGame[0].playerName }} & spelare O: {{ playersInGame[1].playerName }}</p>
    <p>Din tur: ...</p>
    <section id="playingField">
    <div @click="makeMove(i)" class="square" v-for="(board, i) in playingField" key="i">{{ board.text }}</div>
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