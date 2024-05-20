<script setup lang="ts">
import { ref } from "vue";
import SetPlayersPage from "./components/SetPlayersPage.vue"
import PlayingFieldPage from "./components/PlayingFieldPage.vue"

const state = ref({
  showPlayingField: false,
});

function handleChangeView() {
  state.value.showPlayingField = !state.value.showPlayingField;
};

</script>

<template>
    <PlayingFieldPage v-if="state.showPlayingField" />
    <SetPlayersPage v-else @handel-change-view="handleChangeView"/>
</template>

<style scoped>

</style>
