<script setup lang='ts'>
import AddPlayersForm from "./AddPlayersForm.vue"

defineEmits<{
  (e: "handelChangeView"): void;
}>();

</script>

<template>
    <AddPlayersForm 
    @change-view="$emit('handelChangeView')"
    />
</template>

<style scoped></style>