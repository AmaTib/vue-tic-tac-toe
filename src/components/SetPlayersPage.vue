<script setup lang='ts'>
import AddPlayersForm from "./AddPlayersForm.vue"

defineEmits<{
  (e: "handelChangeView", arrLength:number): void;
}>();

</script>

<template>
    <AddPlayersForm 
    @change-view="(arrLength) => {$emit('handelChangeView', arrLength)}"
    />
</template>

<style scoped></style>