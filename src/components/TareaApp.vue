<template>
  <h1>App Tareas</h1>
  <TareaForm />

  <TareaItem v-for="tarea in tareas" :key="tarea.id" :tarea="tarea" />

  <div v-if="tareas.length == 0" class="alert alert-dark mt-3">
    Sin tareas pendientes 👀
  </div>
</template>

<script setup>
import { ref } from "@vue/reactivity";
import { provide, watchEffect } from "@vue/runtime-core";
import TareaForm from "./TareaForm.vue";
import TareaItem from "./TareaItem.vue";

//se declara el array donde se guardaran las tareas
const tareas = ref([]);

//se extiende la constante "tareas" con "provide" para que otros componentes tengan acceso a ella
provide("tareas", tareas);

//Se evalua si ya existe un item "tareas" en el local storage
if (localStorage.getItem("tareas")) {
  //Si existe, el array "tareas" sera igual al item del localstorage
  tareas.value = JSON.parse(localStorage.getItem("tareas"));
}

//El watchEffect introducira el valor del array "tareas" en el item del localstorage cada vez que el array cambie su valor.
watchEffect(() => {
  localStorage.setItem("tareas", JSON.stringify(tareas.value));
});
</script>

<style></style>
