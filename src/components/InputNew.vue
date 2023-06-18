<script setup>
import { ref} from "vue";
//const props = defineProps(["onNewItem"]);
const text = ref("");
const emits = defineEmits(["onNewItem"]);

function handleKeyDown(evt) {
  if(text.value === "" && evt.key !== "Enter"){
    return;// Si el campo de texto está vacío y la tecla presionada no es "Enter", se sale de la función sin realizar ninguna acción adicional.
  }

  if (evt.key === "Enter") {
    if(text.value !== ""){
      emits("onNewItem", text);
      text.value = "";
    }else{
      alert("It is necessary to enter the name of the task to be able to be added 😣")
    }
  }

}
</script>

<template><input v-model="text" @keydown="handleKeyDown" placeholder="Add new task" /></template>

<style scoped></style>