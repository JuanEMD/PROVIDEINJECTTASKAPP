<template>
    <form @submit.prevent="agregarTarea">
        <input
        type="text"
        class="form-control my-2"
        v-model.trim="texto">

        <button type="submit" class="btn btn-primary w-100">Agregar</button>
    </form>
</template>

<script setup>
import { inject, ref } from "@vue/runtime-core";

    const texto = ref('')
    const tareas = inject('tareas')
    
    const agregarTarea = () => {
        if(texto.value === ''){
            return console.log("texto vacio")
        }
        const tarea = {
            id:Date.now(),
            texto: texto.value,
            estado: false
        }

        tareas.value.push(tarea)
        texto.value = ''
    }
</script>

<style>

</style>