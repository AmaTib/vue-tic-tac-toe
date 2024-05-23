<script setup lang="ts">
import { computed, ref } from "vue";
import { Player } from "../models/Player";

interface PlayersProps {
  playersInGame: Player[];
}
const props = defineProps<PlayersProps>();

const currentPlayer = ref<Player>(props.playersInGame[0]);
const playingField = ref([
  { text: "" },
  { text: "" },
  { text: "" },
  { text: "" },
  { text: "" },
  { text: "" },
  { text: "" },
  { text: "" },
  { text: "" },
]);
const gameOver = ref(false);
const theWinner = computed(() => calculateWinner(playingField.value));

function makeMove(i: number) {
  if (gameOver.value === true) return;

  if (playingField.value[i].text !== "") {
    return;
  }

  playingField.value[i].text = currentPlayer?.value?.playerSymbol!;

  if (currentPlayer.value === props.playersInGame[0]) {
    currentPlayer.value = props.playersInGame[1];
  } else {
    currentPlayer.value = props.playersInGame[0];
  }
}

interface Square {
  text: string;
}
function calculateWinner(squares: Square[]): string | null {
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
    if (
      squares[a].text &&
      squares[a].text === squares[b].text &&
      squares[a].text === squares[c].text
    ) {
      gameOver.value = true;
      return squares[a].text;
    }
  }
  return null;
}

function isTie(): boolean {
  return (
    !theWinner.value && playingField.value.every((square) => square.text !== "")
  );
}

function resetGame() {
  playingField.value.forEach((square) => {
    square.text = "";
  });
  currentPlayer.value =
    props.playersInGame[Math.floor(Math.random() * props.playersInGame.length)];

  gameOver.value = false;
}
</script>

<template>
  <h4>Let the game begin</h4>

  <div class="displayPlayers">
    <p>Spelare X: {{ playersInGame[0].playerName }}</p>
    <p>Spelare O: {{ playersInGame[1].playerName }}</p>
  </div>

  <p v-if="gameOver === false && !isTie()">
    Din tur <span>{{ currentPlayer?.playerName }}</span>
  </p>
  <h2 v-if="theWinner">{{ theWinner }}: vann</h2>
  <h2 v-if="isTie()">Oavgjort</h2>

  <section id="playingField">
    <div
      @click="makeMove(i)"
      class="square"
      v-for="(square, i) in playingField"
      :key="i"
    >
      {{ square.text }}
    </div>
  </section>

  <button @click="resetGame">Nytt spel</button>
</template>

<style scoped>
.displayPlayers {
  display: flex;
  justify-content: center;
  gap: 1em;
  margin-bottom: 1em;
}

span {
  background-color: rgb(252, 247, 218);
  padding: 0 10px;
}

#playingField {
  display: grid;
  margin: 0 auto;
  width: fit-content;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: repeat(3, 1fr);
  gap: 0.5em;
  margin-bottom: 2em;
  margin-top: 1em;
}
.square {
  background: rgba(255, 255, 255, 0.2);
  border-radius: 8px;
  box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
  backdrop-filter: blur(5px);
  -webkit-backdrop-filter: blur(5px);
  border: 1px solid rgba(255, 255, 255, 0.3);

  height: 2em;
  width: 2em;
  display: flex;
  justify-content: center;
  align-items: center;

  font-family: "Pally", sans-serif;
  font-size: 2em;
  color: #0f1656;
}
</style>
