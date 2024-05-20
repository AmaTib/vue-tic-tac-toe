<script setup lang='ts'>
import { Player } from "../models/Player";
import AddPlayersForm from "./AddPlayersForm.vue"

defineEmits<{
  (e: "handelChangeView", arrLength:number): void;
}>();

interface PlayersProps{
  players: Player[]
}

defineProps<PlayersProps>();

</script>

<template>
    <AddPlayersForm 
    :players="players"
    @change-view="(arrLength) => {$emit('handelChangeView', arrLength)}"
    />
</template>

<style scoped></style>