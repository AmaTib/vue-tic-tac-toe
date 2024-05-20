<script setup lang="ts">
import { ref } from "vue";
import SetPlayersPage from "./components/SetPlayersPage.vue"
import PlayingFieldPage from "./components/PlayingFieldPage.vue"
import { Player } from "./models/Player";

const state = ref({
  showPlayingField: false,
});

const players = ref<Player[]>([])

function handleChangeView(arrLength:number) {
  if (arrLength > 1) {
    state.value.showPlayingField = !state.value.showPlayingField;
  }
  else{
    alert("måste finnas två spelare")
  }
};

</script>

<template>
    <PlayingFieldPage  v-if="state.showPlayingField" />
    <SetPlayersPage :players="players" v-else @handel-change-view="handleChangeView"/>
</template>

<style scoped>

</style>
