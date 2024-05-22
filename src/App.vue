<script setup lang="ts">
import { ref } from "vue";
import SetPlayersPage from "./components/SetPlayersPage.vue";
import PlayingFieldPage from "./components/PlayingFieldPage.vue";
import { Player } from "./models/Player";

const state = ref({
  showPlayingField: false,
});

const players = ref<Player[]>([]);

function handleChangeView(arrLength: number) {
  if (arrLength > 1) {
    state.value.showPlayingField = !state.value.showPlayingField;
  } else {
    alert("måste finnas två spelare");
  }
}
</script>

<template>
  <h1>
    The great game <br />
    of <br />
    <span>Tic</span> Tac <span>Toe</span>
  </h1>
  <PlayingFieldPage :players-in-game="players" v-if="state.showPlayingField" />
  <SetPlayersPage
    :players="players"
    v-else
    @handel-change-view="handleChangeView"
  />
</template>

<style scoped>
h1 {
  font-family: "Array", sans-serif;
  font-size: 2em;
  margin-bottom: 1em;
}
span {
  color: #2a38ae;
}
</style>
