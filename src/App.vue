<script setup lang="ts">
import { ref } from "vue";
import SetPlayersPage from "./components/SetPlayersPage.vue"
import PlayingFieldPage from "./components/PlayingFieldPage.vue"

const state = ref({
  showPlayingField: false,
});

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
    <PlayingFieldPage v-if="state.showPlayingField" />
    <SetPlayersPage v-else @handel-change-view="handleChangeView"/>
</template>

<style scoped>

</style>
