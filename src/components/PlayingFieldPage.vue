<script setup lang='ts'>
import { ref } from 'vue';

let playingField = ref([{text:""},{text:""},{text:""},{text:""},{text:""},{text:""},{text:""},{text:""},{text:""}])

const square = ""

function makeMove(i:number){
    if (true){
        playingField.value[i].text = "X"
    }
}

</script>

<template>
    <h4>Let the game begin</h4>
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